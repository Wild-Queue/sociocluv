<script lang="ts">
	import { onMount } from 'svelte';
	import Card from '$lib/Card.svelte';
	let showHeader = false;
	onMount(() => {
		if (sessionStorage.getItem('authorized') == 'true') {
			showHeader = true;
		}
	});
</script>

<Card>
	<div slot="card-body">
		<nav>
			{#if !showHeader}
				<a href="/">Log In</a>
			{/if}
			{#if showHeader}
				<a href="/elonmusk">Profile</a>
				<a href="/home">Feed</a>
				<a href="/elonmusk/status/1">Single Tweet</a>
				<a href="/about">About</a>
			{/if}
		</nav>
	</div>
</Card>

<style>
	nav {
		display: flex;
		justify-content: space-between;
		align-items: center;
		padding: 1rem;
		background: white;
	}
	nav a {
		color: #333;
		text-decoration: none;
		margin: 0 0.5rem;
	}
	nav a:hover {
		color: #555;
	}
</style>
