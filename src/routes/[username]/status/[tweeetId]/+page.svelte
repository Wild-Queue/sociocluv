<script lang='ts'>
    import Post from "$lib/Post.svelte";
    import Comments from "$lib/Comments.svelte";
</script>


<svelte:head>
	<title>Single Tweet</title>
	<meta name="description" content="tweet" />
</svelte:head>


<div>
    <!--<Post author="Arseniy"/>-->
    <Comments/>
</div>