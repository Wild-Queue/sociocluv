<script lang='ts'>
    import Post from "$lib/Post.svelte";

	import { onMount, onDestroy } from "svelte";
	let listElement:HTMLDivElement;

	let items:string[] = ["Arseniy", "Nikita", "Bob", "Sam", "Kate", "Watter", "Kamble", "Nani","Arseniy", "Nikita", "Bob", "Sam", "Kate", "Watter", "Kamble", "Nani","Arseniy", "Nikita", "Bob", "Sam", "Kate", "Watter", "Kamble", "Nani"];

	for (let index = 0; index < 20; index++) {
		items = [...items, `${items[index]}`];
	}

	// Add 20 items.
	function loadMore() {
		for (var index = 0; index < 20; index++) {
			items = [...items, `${items[index]}`];
		}
	}
</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="home" />
</svelte:head>

<h1 >Explore the world of Sociocluv:</h1>



<div bind:this={listElement} >
	{#each items as item}
		<!-- <Post author={item}/> -->
	{/each}
</div>

<div id="button-wrapper">
	<button on:click={loadMore}>Load more</button>
</div>

<style>
button {
		font-size:medium;
		border: medium none;
		background-image: none;
		background: transparent;
		background-color: transparent;
		color: blue;
		cursor: pointer;
	}
#button-wrapper{
	inline-size: max-content;
	
	padding: 10px 0px 15px 0px;
}
</style>