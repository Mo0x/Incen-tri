<script lang="ts">
	import { page } from '$app/stores';
 	import "../app.css";
  
	const tabs = [
	  { name: 'Home',    href: '/',        icon: '🏠' },
	  { name: 'Map',     href: '/map',     icon: '🗺️' },
	  { name: 'League',  href: '/league',  icon: '🏆' },
	  { name: 'Profile', href: '/profile', icon: '👤' }
	];
  
	function isActive(pathname: string, href: string)
	{
	  // exact match for now ("/", "/map", "/league", "/profile")
	  return pathname === href;
	}
  </script>
  
  <div class="app-shell">
	<main class="app-main">
	  <slot />
	</main>

	<a class="scan-button" href="/scan">
	  <span class="scan-icon">📷</span>
	  <span class="scan-label">Scan / Collecter</span>
	</a>
  
	<nav class="bottom-nav">
	  {#each tabs as tab}
		{#if $page.url.pathname}
		  <a
			href={tab.href}
			class:active={isActive($page.url.pathname, tab.href)}
		  >
			<span class="icon">{tab.icon}</span>
			<span class="label">{tab.name}</span>
		  </a>
		{/if}
	  {/each}
	</nav>
  </div>
  
  <style>
	.app-shell {
	  min-height: 100vh;
	  display: flex;
	  flex-direction: column;
	  background: radial-gradient(circle at top, rgba(79, 200, 117, 0.08), transparent), var(--color-bg);
	  color: var(--color-ink);
	  font-family: "Inter", system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
	}

	.app-main {
	  flex: 1;
	  padding: 1rem;
	  padding-bottom: 4.5rem;
	  box-sizing: border-box;
	}

	.scan-button {
	  position: fixed;
	  left: 50%;
	  bottom: 4.8rem;
	  transform: translateX(-50%);
	  display: inline-flex;
	  align-items: center;
	  gap: 0.4rem;
	  padding: 0.85rem 1.4rem;
	  border-radius: 999px;
	  background: linear-gradient(120deg, var(--color-accent), var(--color-accent-strong));
	  color: #fff;
	  font-weight: 600;
	  text-decoration: none;
	  box-shadow: 0 16px 32px rgba(4, 33, 19, 0.25);
	  z-index: 5;
	}

	.scan-icon {
	  font-size: 1.1rem;
	}

	@media (max-width: 640px) {
	  .scan-button {
	    bottom: 5.1rem;
	    padding: 0.75rem 1.2rem;
	  }
	}

	.bottom-nav {
	  position: sticky;
	  bottom: 0;
	  left: 0;
	  right: 0;
	  height: 3.9rem;
	  display: flex;
	  border-top: 1px solid rgba(6, 38, 19, 0.12);
	  background: rgba(255, 255, 255, 0.92);
	  backdrop-filter: blur(18px);
	  box-shadow: 0 -6px 30px rgba(4, 33, 19, 0.08);
	}

	.bottom-nav a {
	  flex: 1;
	  display: flex;
	  flex-direction: column;
	  align-items: center;
	  justify-content: center;
	  font-size: 0.78rem;
	  color: rgba(5, 27, 19, 0.55);
	  gap: 0.1rem;
	  font-weight: 500;
	}

	.bottom-nav a .icon {
	  font-size: 1.25rem;
	  line-height: 1;
	}

	.bottom-nav a.active {
	  color: var(--color-accent-strong);
	}

	.bottom-nav a.active .icon {
	  transform: translateY(-1px);
	}
  </style>
  
