<script lang="ts">
	export let data;
	const image_src = "https://pbs.twimg.com/profile_images/1590968738358079488/IY9Gx6Ok_400x400.jpg";
	import Post from '$lib/Post.svelte';
	import Header from '$lib/Header.svelte';
	import {page } from '$app/stores'
	$page.params
</script>

<svelte:head>
	<title>Username</title>
	<meta name="description" content="Username" />
</svelte:head>

<div id="top-container" >
<Header/>
<div id="post-author-photo" style="margin-top:30px;">
	<img id="photo" src={image_src} alt="profile avatar" style="width:100%;" />
</div>

<span>Elon Musk</span>
<a href="/{data.username}">
	<span>@{data.username}</span>
</a>
<div style="max-width:300px;margin-top:20px;margin-bottom:20px;text-indent:30px;">Elon Musk's Twitter profile is a reflection of his eclectic personality, his bold ideas, and his vision for the future of technology. At the top of his profile, you'll find a picture of his face, which is often accompanied by a witty or provocative comment.</div>
</div>
<h2 style="margin-bottom:0px;margin-top:50px;">Tweets</h2>
<Post/>
<Post/>
<Post/>


<style>
#top-container{
	margin-top: 30px;
	display: flex;
	flex-direction: column;
	align-items: center;
	border-radius: 10px;
	width:600px;
	overflow:hidden;
	box-shadow:  rgba(0, 0, 0, 0.07) 0px -100px 100px -40px;
  	background-image: linear-gradient(to bottom, rgb(255, 255, 255) 0%, rgba(255, 255, 255, 0) 100%); /* Set a linear-gradient background with initial opacity of 1 at the top and 0 at the bottom */
  	background-size: 100% 100%; /* Set the background size to cover the entire div element */
}

#post-author-photo{
    width:88px;
    height:88px;
    margin-top: 3px;
    margin-bottom: 3px;
    border-radius: 30px;
    overflow: hidden;
}
</style>