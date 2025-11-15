<script lang="ts">
  import { onMount } from 'svelte';

  type Entry = {
      rank: number;
      name: string;
      score?: number;
      isUser?: boolean;
  };

  // TODO: plug this into your real profile username
  let userName = 'Ton pseudo';

  // default: user is private
  let isPublic = false;
  let hasMounted = false;

  const baseLeaderboard: Entry[] = [
      { rank: 1, name: 'XXX' },
      { rank: 2, name: 'YYYY' },
      // ...
      { rank: 68, name: 'aaaaa' },
      { rank: 69, name: 'temporary user placement', isUser: true },
      { rank: 70, name: 'yyyyyyyyyyyyyyyyyy' }
  ];

  onMount(() =>
  {
      hasMounted = true;
      const stored = localStorage.getItem('leaderboard_public');
      if (stored !== null)
          isPublic = stored === 'true';
  });

  // Persist the choice locally so it sticks across refreshes
  $: if (hasMounted)
  {
      localStorage.setItem('leaderboard_public', String(isPublic));
  }

  // Build the displayed leaderboard:
  // your row (rank 69) swaps between anonymous + public name
  $: leaderboard = baseLeaderboard.map((entry) =>
  {
      if (entry.isUser)
      {
          return {
              ...entry,
              name: isPublic ? userName : 'Temporary user placement'
          };
      }
      return entry;
  });

  $: userEntry = leaderboard.find((entry) => entry.isUser);

  const quickNotes = [
      'Le top 10 partage un update par semaine.',
      'Tu peux quitter le mode privé à tout moment.',
      'Le podium gagne une surprise en fin de mois.'
  ];

  $: heroStats = [
      {
          label: 'Ta position',
          value: userEntry ? `#${userEntry.rank}` : '--'
      },
      {
          label: 'Visibilité',
          value: isPublic ? 'Publique' : 'Anonyme'
      },
      {
          label: 'Objectif du mois',
          value: '#50'
      }
  ];
</script>

<section class="page leaderboard-page">
  <div class="page-inner">
    <header class="card card--highlight">
      <div class="section-header">
        <div>
          <span class="chip">Classement pilote</span>
          <h1>Leaderboard</h1>
          <p>Par défaut tu es anonyme. Change de statut en un clic.</p>
        </div>
        <button class="toggle-btn toggle-btn--ghost" type="button" on:click={() => (isPublic = !isPublic)}>
          {#if isPublic}
            👀 Visible publiquement
          {:else}
            🔒 Rester discret
          {/if}
        </button>
      </div>
      <div class="stat-grid">
        {#each heroStats as stat}
          <article class="stat-card">
            <h3>{stat.value}</h3>
            <p>{stat.label}</p>
          </article>
        {/each}
      </div>
    </header>

    <section class="section">
      <div class="card card--hoverable">
        <div class="section-header">
          <h2 class="section-title">Classement général</h2>
          <span class="chip chip--muted">
            {isPublic ? 'Pseudo visible' : 'En privé'}
          </span>
        </div>
        <div class="table-wrapper">
          <table class="table">
            <thead>
              <tr>
                <th>#</th>
                <th>Nom</th>
              </tr>
            </thead>
            <tbody>
              {#each leaderboard as entry}
                <tr class:me={entry.isUser}>
                  <td>{entry.rank}</td>
                  <td>
                    {#if entry.isUser}
                      {#if isPublic}
                        {entry.name} <span class="badge">toi</span>
                      {:else}
                        {entry.name} <span class="badge is-muted">toi (privé)</span>
                      {/if}
                    {:else}
                      {entry.name}
                    {/if}
                  </td>
                </tr>
              {/each}
            </tbody>
          </table>
        </div>
      </div>
    </section>

    <section class="section profile-grid">
      <div class="card">
        <div class="section-header">
          <h2 class="section-title">Ta progression</h2>
          <span class="pill">updates auto</span>
        </div>
        <ul class="impact-list">
          <li>
            <span>Rang actuel</span>
            <strong>{userEntry ? `#${userEntry.rank}` : '--'}</strong>
          </li>
          <li>
            <span>Objectif prochain palier</span>
            <strong>#60</strong>
          </li>
          <li>
            <span>Partage public</span>
            <strong>{isPublic ? 'activé' : 'désactivé'}</strong>
          </li>
        </ul>
      </div>
      <div class="card trivia-card">
        <div class="section-header">
          <h2 class="section-title">Notes communauté</h2>
          <span class="pill">idées comm'</span>
        </div>
        <ul class="trivia-list">
          {#each quickNotes as note, idx}
            <li>
              <strong>{idx + 1}.</strong>
              <span>{note}</span>
            </li>
          {/each}
        </ul>
      </div>
    </section>
  </div>
</section>

<style>
  .leaderboard-page tr.me {
      background: rgba(47, 184, 117, 0.08);
  }

  .leaderboard-page .badge {
      margin-left: 0.4rem;
  }

  .leaderboard-page table tr td:first-child,
  .leaderboard-page table tr th:first-child {
      width: 60px;
  }
</style>
