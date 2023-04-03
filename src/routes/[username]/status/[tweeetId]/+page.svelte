<script lang='ts'>
    import Post from "$lib/Post.svelte";
import Header from "$lib/Header.svelte";
</script>


<svelte:head>
	<title>Single Tweet</title>
	<meta name="description" content="tweet" />
</svelte:head>

<Header/>
<div>
    <Post/>
</div>