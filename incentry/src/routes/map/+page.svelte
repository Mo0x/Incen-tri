<script lang="ts">
  import mapImage from "./Map_Collect_Point.png";

  const coverage = [
    { label: "Points actifs", value: "38" },
    { label: "Quartiers bêta", value: "6" },
    { label: "Bornes organiques", value: "12" }
  ];

  const focusAreas = [
    {
      title: "Maison du Projet",
      note: "Hub principal + QR onboarding",
      status: "7j/7"
    },
    {
      title: "Marché du Boulingrin",
      note: "Dépot pilote compost & recyclage",
      status: "samedi"
    },
    {
      title: "Quartier Saint-Anne",
      note: "Collecte mobile tous les mardis",
      status: "mobile"
    }
  ];

  const tips = [
    "Zoom sur ta rue pour afficher les horaires et les flux acceptés.",
    "Les zones vertes indiquent les bacs organiques avec QR.",
    "Besoin d'un nouveau point ? Indique-le via la messagerie profil."
  ];
</script>

<svelte:head>
  <title>Carte des points de collecte</title>
</svelte:head>

<section class="page map-page">
  <div class="page-inner">
    <header class="card card--highlight">
      <div class="section-header">
        <div>
          <span class="chip">Territoire pilote</span>
          <h1>Carte des points de collecte</h1>
        </div>
        <span class="pill">Mise à jour hebdo</span>
      </div>
      <p>
        Visualise les points QR et les bornes organiques du Grand Reims. Chaque
        carte peut être remplacée dès que l'équipe carto publie une nouvelle
        version.
      </p>
      <div class="stat-grid">
        {#each coverage as item}
          <article class="stat-card">
            <h3>{item.value}</h3>
            <p>{item.label}</p>
          </article>
        {/each}
      </div>
    </header>

    <section class="section">
      <div class="card map-card">
        <img src={mapImage} alt="Carte des points de collecte du Grand Reims" />
        <p>
          Les zones lumineuses indiquent les points actifs. Ajoute ici une image
          plus récente ou une carte interactive quand elle sera prête.
        </p>
      </div>
    </section>

    <section class="section profile-grid">
      <div class="card">
        <div class="section-header">
          <h2 class="section-title">Points focus</h2>
          <span class="chip chip--muted">Modifie selon tes priorités</span>
        </div>
        <ul class="legend-list">
          {#each focusAreas as area}
            <li>
              <div>
                <strong>{area.title}</strong>
                <p>{area.note}</p>
              </div>
              <span class="badge">{area.status}</span>
            </li>
          {/each}
        </ul>
      </div>
      <div class="card trivia-card">
        <div class="section-header">
          <h2 class="section-title">Tips utilisateurs</h2>
          <span class="pill">à pusher dans l'app</span>
        </div>
        <ul class="trivia-list">
          {#each tips as tip, index}
            <li>
              <strong>{index + 1}.</strong>
              <span>{tip}</span>
            </li>
          {/each}
        </ul>
      </div>
    </section>
  </div>
</section>
