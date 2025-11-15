<script lang="ts">
  import qrCodeImg from './QRcode.png';
  import bacImg from './bac_de_tri.jpg';
</script>

<svelte:head>
  <title>Scan & Collecter · Incen'tri</title>
</svelte:head>

<section class="page scan-page">
  <div class="page-inner">
    <header class="card card--highlight scan-hero">
      <div class="scan-copy">
        <span class="chip">Scan / Collecte</span>
        <h1>Prépare ton dépôt</h1>
        <p>Scanne ton QR, on t'identifie, puis on dépose dans la borne.</p>
      </div>
    </header>

    <div class="card scan-grid">
      <div class="scan-qr">
        <img src={qrCodeImg} alt="QR code Incentri" />
      </div>
      <div class="scan-arrow">➡️</div>
      <div class="scan-photo">
        <img src={bacImg} alt="" />
      </div>
    </div>
  </div>
</section>

<style>
  .scan-grid {
    margin-top: 1rem;
    display: grid;
    grid-template-columns: repeat(3, minmax(0, 1fr));
    align-items: center;
    gap: 1.25rem;
  }

  .scan-qr img {
    width: 100%;
    max-width: 220px;
    border-radius: 18px;
    border: 1px solid rgba(5, 27, 19, 0.1);
    box-shadow: 0 8px 22px rgba(4, 33, 19, 0.15);
  }

  .scan-photo img {
    width: 100%;
    border-radius: 18px;
    object-fit: cover;
    height: 240px;
  }

  .scan-arrow {
    text-align: center;
    font-size: clamp(2.5rem, 3vw, 3.5rem);
  }

  @media (max-width: 700px) {
    .scan-grid {
      grid-template-columns: 1fr;
      text-align: center;
    }

    .scan-photo img {
      height: auto;
    }
  }
</style>
