<script>
	import { page } from '$app/stores';
  
	const tabs = [
	  { name: 'Home',    href: '/',        icon: '🏠' },
	  { name: 'Map',     href: '/map',     icon: '🗺️' },
	  { name: 'League',  href: '/league',  icon: '🏆' },
	  { name: 'Profile', href: '/profile', icon: '👤' }
	];
  
	function isActive(pathname, href)
	{
	  // exact match for now ("/", "/map", "/league", "/profile")
	  return pathname === href;
	}
  </script>
  
  <div class="app-shell">
	<main class="app-main">
	  <slot />
	</main>
  
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
	  background: #0b1f16; /* dark green background for the app */
	  color: #f9f9f9;
	  font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
	}
  
	.app-main {
	  flex: 1;
	  padding: 1rem;
	  padding-bottom: 4.5rem; /* make room for bottom nav */
	  box-sizing: border-box;
	}
  
	.bottom-nav {
	  position: sticky;
	  bottom: 0;
	  left: 0;
	  right: 0;
	  height: 3.8rem;
	  display: flex;
	  border-top: 1px solid rgba(255, 255, 255, 0.1);
	  background: rgba(7, 12, 10, 0.98);
	  backdrop-filter: blur(10px);
	}
  
	.bottom-nav a {
	  flex: 1;
	  display: flex;
	  flex-direction: column;
	  align-items: center;
	  justify-content: center;
	  text-decoration: none;
	  font-size: 0.75rem;
	  color: rgba(255, 255, 255, 0.6);
	  gap: 0.1rem;
	}
  
	.bottom-nav a .icon {
	  font-size: 1.2rem;
	  line-height: 1;
	}
  
	.bottom-nav a.active {
	  color: #b9ff84; /* active green */
	  font-weight: 600;
	}
  
	.bottom-nav a.active .icon {
	  transform: translateY(-1px);
	}
  </style>
  