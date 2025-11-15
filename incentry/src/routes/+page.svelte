<script lang="ts">
  const user = {
    name: "Lina",
    city: "Reims",
    tier: "Quartier pionnier",
    tierLevel: 2,
    tierLabel: "Graine tenace",
    lp: 820,
    tierGoalLP: 1000,
    weekPoints: 420,
    streak: 4,
    stats: [
      { label: "collectes effectuées", value: "24" },
      { label: "dépôts ce mois", value: "7" },
      { label: "voisins inspirés", value: "3" }
    ]
  };

  const goals = [
    {
      tag: "Starter",
      title: "Scanne ton premier QR code",
      description: "Débloque ta carte membre et gagne un badge de bienvenue.",
      progress: 0.35
    },
    {
      tag: "Habitude",
      title: "Dépose 4 fois ce mois-ci",
      description: "Récompense surprise dès la troisième visite.",
      progress: 0.6
    },
    {
      tag: "Impact",
      title: "Invite un·e voisin·e",
      description: "Partage ton code et suivez vos progrès ensemble.",
      progress: 0.15
    },
    {
      tag: "Nouveauté",
      title: "Teste la borne organique",
      description: "Fais un dépôt d'organiques et raconte-nous.",
      progress: 0.05
    }
  ];

  const intensives = [
    {
      type: "Challenge",
      title: "Scan & Go",
      description:
        "Scanne ton tout premier QR code sur site pour débloquer l'espace récompenses.",
      lpReward: 80,
      tierRange: "Tier 0-2"
    },
    {
      type: "Dépôt",
      title: "Première collecte organique",
      description:
        "Dépose au moins 2 kg de biodéchets au point pilote et gagne +50 pts.",
      lpReward: 120,
      tierRange: "Tier 3-5"
    },
    {
      type: "Communauté",
      title: "Story compost",
      description:
        "Prends une photo de ton bac propre, partage-la et tague @incentri.",
      lpReward: 160,
      tierRange: "Tier 6-9"
    }
  ];

  const trivia = [
    "60 % du sac gris est encore composé d'organique – les détourner réduit par 2 les tournées camions.",
    "Un compost bien aéré chauffe naturellement jusqu'à 60°C, ce qui élimine la plupart des pathogènes.",
    "Composter 1 kg de marc de café économise l'équivalent d'une ampoule LED allumée pendant 24 h.",
    "Le tri des biodéchets permet d'éviter 30 kg de CO₂ par foyer et par an en moyenne."
  ];

  const tierProgress = Math.min(user.lp / user.tierGoalLP, 1);

  const padIndex = (value: number) => `${value}`.padStart(2, "0");
</script>

<svelte:head>
  <title>Accueil · Incen'tri</title>
</svelte:head>

<section class="page home">
  <div class="page-inner">
    <header class="card card--highlight home-hero">
      <div class="hero-top">
        <div class="hero-copy">
          <span class="chip">Bonjour {user.name}</span>
          <h1>Ton compost change le quartier</h1>
          <p>{user.city} · {user.tier}</p>
        </div>
        <div class="hero-score">
          <span>Points semaine</span>
          <strong>{user.weekPoints}</strong>
          <small>{user.streak} semaines d'affilée</small>
        </div>
      </div>
      <div class="tier-status">
        <div class="level-badge">T{user.tierLevel}</div>
        <div class="tier-details">
          <strong>{user.tierLabel}</strong>
          <span>Palier {user.tierLevel} / 9</span>
          <span>{user.lp} LP · objectif {user.tierGoalLP} LP</span>
          <div class="tier-progress">
            <span style={`width: ${tierProgress * 100}%`}></span>
          </div>
        </div>
        <span class="lp-chip">{user.lp} LP</span>
      </div>
      <div class="stat-grid">
        {#each user.stats as stat}
          <article class="stat-card">
            <h3>{stat.value}</h3>
            <p>{stat.label}</p>
          </article>
        {/each}
      </div>
    </header>

    <section class="section home-split">
      <div class="card card--hoverable">
        <div class="section-header">
          <h2 class="section-title">Objectifs du moment</h2>
        </div>
        <ul class="goals-grid goals-grid--2col">
          {#each goals as goal}
            <li class="goal-card">
              <div class="goal-meta">
                <span class="chip chip--muted">{goal.tag}</span>
                <span>{Math.round(goal.progress * 100)}%</span>
              </div>
              <h3>{goal.title}</h3>
              <p>{goal.description}</p>
              <div class="progress-track">
                <span
                  class="progress-value"
                  style={`width: ${goal.progress * 100}%`}
                ></span>
              </div>
            </li>
          {/each}
        </ul>
      </div>

      <div class="card card--hoverable">
        <div class="section-header">
          <h2 class="section-title">Incitation du moment</h2>
        </div>
        <ul class="action-list">
          {#each intensives as action}
            <li>
              <div class="chip">{action.type}</div>
              <strong>{action.title}</strong>
              <span>{action.description}</span>
              <div class="goal-meta">
                <span>{action.tierRange}</span>
                <span class="lp-chip">+{action.lpReward} LP</span>
              </div>
            </li>
          {/each}
        </ul>
      </div>
    </section>

    <section class="section">
      <div class="section-header">
        <h2 class="section-title">Trivia recyclage & compost</h2>
        <span class="pill">À piocher pour les stories</span>
      </div>
      <div class="card trivia-card">
        <ul class="trivia-list">
          {#each trivia as fact, index}
            <li>
              <strong>{padIndex(index + 1)}</strong>
              <span>{fact}</span>
            </li>
          {/each}
        </ul>
      </div>
    </section>

  </div>
</section>
