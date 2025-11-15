<script lang="ts">
  type Coupon = {
    id: string;
    title: string;
    description: string;
    tier: number;
    partner: string;
    code: string;
    collected?: boolean;
  };

  type ProfileTab = "stats" | "coupons";

  const profile = {
    name: "Lina",
    id: "#INC-3847",
    district: "Saint-Anne",
    joined: "Mars 2024",
    status: "Ambassadrice beta",
    tierLevel: 2,
    tierLabel: "Graine tenace",
    lp: 820,
    tierGoalLP: 1000
  };

  const deepStats = [
    { label: "Total dépôts", value: "42" },
    { label: "collectes effectuées", value: "24" },
    { label: "Semaines actives", value: "18" }
  ];

  const impactBreakdown = [
    { label: "Organique détourné", value: "68 %" },
    { label: "Tri recyclage", value: "22 %" },
    { label: "Sensibilisation", value: "10 %" }
  ];

  const upcoming = [
    {
      title: "Badge QR master",
      detail: "Scanner 10 QR différents – 2 restants"
    },
    {
      title: "Pack compost maison",
      detail: "Partager 3 photos propres du bac"
    }
  ];

  const faq = [
    {
      q: "Comment changer mes objectifs ?",
      a: "Passe par marketing@incentri.com ou via le back-office."
    },
    {
      q: "Puis-je exporter mes données ?",
      a: "Oui, onglet données – CSV généré en 1 clic (à brancher)."
    }
  ];

  const tierMilestones = [
    { level: 0, label: "Racine", reward: "Accès aux points publics" },
    { level: 1, label: "Pousse", reward: "Badge QR de bienvenue" },
    { level: 2, label: "Graine tenace", reward: "+5 % LP sur intensifs" },
    { level: 3, label: "Plantule", reward: "Coupons cafés locaux" },
    { level: 4, label: "Canopée", reward: "+1 accès événement" },
    { level: 5, label: "Ruche", reward: "Kit compost maison" },
    { level: 6, label: "BiodiverCity", reward: "Collecte à domicile test" },
    { level: 7, label: "Grainothèque", reward: "Pack graines locales" },
  ];

  let activeTab: ProfileTab = "stats";

  let coupons: Coupon[] = [
    {
      id: "cafe",
      title: "Café bio offert",
      description: "Un expresso chez Bloom Café après 20 collectes.",
      tier: 2,
      partner: "Bloom Café",
      code: "BLOOM-LINA"
    },
    {
      id: "compost",
      title: "Recharge sacs compost",
      description: "3 sacs kraft premium offerts au prochain dépôt.",
      tier: 3,
      partner: "Recyclerie Reims",
      code: "SAC-TRI-203"
    },
    {
      id: "atelier",
      title: "Atelier compost VIP",
      description: "Place réservée pour l'atelier ambassadeur.",
      tier: 4,
      partner: "Maison du Projet",
      code: "VIP-AMBASS"
    }
  ];

  const tierProgress = Math.min(profile.lp / profile.tierGoalLP, 1);

  function toggleCoupon(id: string)
  {
    coupons = coupons.map((coupon) =>
      coupon.id === id ? { ...coupon, collected: !coupon.collected } : coupon
    );
  }
</script>

<svelte:head>
  <title>Profil · Incen'tri</title>
</svelte:head>

<section class="page profile-page">
  <div class="page-inner">
    <header class="card card--highlight home-hero">
      <div class="hero-top">
        <div class="hero-copy">
          <span class="chip">Compte pilote</span>
          <h1>{profile.name}</h1>
          <p>{profile.status} · {profile.district}</p>
        </div>
        <div class="hero-score">
          <span>ID</span>
          <strong>{profile.id}</strong>
          <small>Depuis {profile.joined}</small>
        </div>
      </div>
      <div class="tier-status">
        <div class="level-badge">T{profile.tierLevel}</div>
        <div class="tier-details">
          <strong>{profile.tierLabel}</strong>
          <span>Palier {profile.tierLevel} / 9</span>
          <span>{profile.lp} LP · objectif {profile.tierGoalLP} LP</span>
          <div class="tier-progress">
            <span style={`width: ${tierProgress * 100}%`}></span>
          </div>
        </div>
        <span class="lp-chip">{profile.lp} LP</span>
      </div>
      <div class="stat-grid">
        {#each deepStats as stat}
          <article class="stat-card">
            <h3>{stat.value}</h3>
            <p>{stat.label}</p>
          </article>
        {/each}
      </div>
    </header>

    <section class="section">
      <div class="card">
        <div class="section-header">
          <h2 class="section-title">Récompenses par tier</h2>
          <span class="pill">0 → 7</span>
        </div>
        <ul class="tier-ladder">
          {#each tierMilestones as tier}
            <li>
              <strong>Tier {tier.level} – {tier.label}</strong>
              <p>{tier.reward}</p>
            </li>
          {/each}
        </ul>
      </div>
    </section>

    <section class="section">
      <div class="section-header">
        <h2 class="section-title">Pilotage du compte</h2>
        <div class="tab-nav">
          <button
            type="button"
            class="tab-button"
            class:is-active={activeTab === "stats"}
            on:click={() => (activeTab = "stats")}
          >
            Stats
          </button>
          <button
            type="button"
            class="tab-button"
            class:is-active={activeTab === "coupons"}
            on:click={() => (activeTab = "coupons")}
          >
            Coupons
          </button>
        </div>
      </div>

      {#if activeTab === "stats"}
        <div class="profile-grid">
          <div class="card">
            <div class="section-header">
              <h3 class="section-title">Répartition impact</h3>
              <span class="chip chip--muted">données fictives</span>
            </div>
            <ul class="impact-list">
              {#each impactBreakdown as item}
                <li>
                  <span>{item.label}</span>
                  <strong>{item.value}</strong>
                </li>
              {/each}
            </ul>
          </div>
          <div class="card">
            <div class="section-header">
              <h3 class="section-title">Récompenses à venir</h3>
              <span class="pill">prévision</span>
            </div>
            <ul class="action-list">
              {#each upcoming as reward}
                <li>
                  <strong>{reward.title}</strong>
                  <span>{reward.detail}</span>
                </li>
              {/each}
            </ul>
          </div>
        </div>

        <div class="card trivia-card">
          <div class="section-header">
            <h3 class="section-title">Questions rapides</h3>
            <span class="pill">FAQ</span>
          </div>
          <ul class="trivia-list">
            {#each faq as item, index}
              <li>
                <strong>{index + 1}.</strong>
                <span>
                  <em>{item.q}</em> — {item.a}
                </span>
              </li>
            {/each}
          </ul>
        </div>
      {:else}
        <div class="card">
          <div class="section-header">
            <h3 class="section-title">Coupons disponibles</h3>
            <span class="pill">collection</span>
          </div>
          <ul class="coupon-list">
            {#each coupons as coupon}
              <li class="coupon-card">
                <strong>{coupon.title}</strong>
                <small>Tier {coupon.tier} · {coupon.partner}</small>
                <p>{coupon.description}</p>
                <footer>
                  <span class="lp-chip">{coupon.code}</span>
                  <button
                    class="btn"
                    type="button"
                    on:click={() => toggleCoupon(coupon.id)}
                    disabled={coupon.collected}
                  >
                    {coupon.collected ? 'Collecté' : 'Collecter'}
                  </button>
                </footer>
              </li>
            {/each}
          </ul>
        </div>
      {/if}
    </section>
  </div>
</section>
  
