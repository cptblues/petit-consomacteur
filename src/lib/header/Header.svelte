<script lang="ts">
	import { page } from '$app/stores';
	import logo from './consomacteur-logo.svg';
</script>

<header>
	<img id="logo" src={logo} alt="SvelteKit" />
	<nav>
		<ul>
			<li class:active={$page.path === '/'}><a sveltekit:prefetch href="/">Accueil</a></li>
			<li class:active={$page.path === '/about'}><a sveltekit:prefetch href="/about">A propos</a></li>
		</ul>
	</nav>
	<div class="cornet">
		Profile
	</div>
</header>

<style>
	header {
		display: flex;
		justify-content: space-between;
		padding: 12px;
		flex-direction: row;
	}

	#logo {
		width: 50px;
		height: 50px;
	}

	nav {
		display: flex;
		justify-content: center;
		font-size: 2rem;
	}

	ul {
		position: relative;
		padding: 0;
		margin: 0;
		width: 100%;
		display: flex;
		flex-direction: row;
		justify-content: center;
		align-items: center;
		list-style: none;
		background-size: contain;
	}

	li {
		position: relative;
		height: 100%;
		margin: 0 4px;
		border-radius: 10px;
	}

	li.active {
		background-color: var(--peach-dark);
	}

	nav a {
		display: flex;
		height: 100%;
		align-items: center;
		padding: 0 1em;
		color: var(--black-coffee);
		font-weight: 700;
		font-size: 0.8rem;
		text-transform: uppercase;
		letter-spacing: 10%;
		text-decoration: none;
		transition: color 0.2s linear;
	}

	a:hover {
		color: var(--pure-white);
	}
</style>
