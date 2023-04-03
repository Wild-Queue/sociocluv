<script>
    import Footer from "$lib/Footer.svelte";
    import Header from "$lib/Header.svelte";

	
</script>

<header>

</header>

<main>
	<slot />
</main>

<footer>
    <Footer />
</footer>

<style>
	main {
		display: flex;
		flex-direction: column;
		
		align-items: center;
	}
    header {
		background-color: #ffffff;
		box-shadow: 0 0 100px -39px rgba(212, 214, 180, 1);
		display: flex;
		justify-content: center;
	}

	footer {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		padding: 12px;
	}
</style>