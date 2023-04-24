<script lang='ts'>
    import Post from "$lib/Post.svelte";
    import Comments from "$lib/Comments.svelte";
    import { page } from '$app/stores';
	let alias_from_url = $page.params.username;
    let tweetId_from_url = $page.params.tweeetId;
</script>


<svelte:head>
	<title>Single Tweet</title>
	<meta name="description" content="tweet" />
</svelte:head>


<div>
    <!--<Post author="Arseniy"/>-->
    <!--<span>Username: {alias_from_url}</span>-->
    <!--<span>TweetId: {tweetId_from_url}</span>-->
    <Comments/>
</div>