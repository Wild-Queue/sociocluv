<script lang="ts">
	const image_src = 'https://cdn-icons-png.flaticon.com/512/168/168726.png';
	import Post from '$lib/Post.svelte';
	import { page } from '$app/stores';
	let alias_from_url = $page.params.username;
	import { io } from 'socket.io-client';
	
	interface Post{
		authorName : string; 
		initPosrID: number;
		likesNum: number;
		postID: number;
		commentsNum: number;
		imageLink : string;
		text: string;
		time: string;
		viewNum: number;
	}

	interface Message {
		username: string;
		message: string;   
	}

	console.log("123");
	//Opening socket
	const socket = io('http://localhost:5050/');
 
	//Request to database
	socket.emit('get-profile-posts', {alias: "aaa"});
	

	let allPosts: Post[] = [];
	let posts:Post[] = [];
	let numberOfLoadedPosts = 0;

	//Waiting for response
	socket.on('get-profile-posts-result', (msg) => {
		console.log(msg);
		console.log(msg['feed']);
		for (let index in msg['feed']) {
			let post: Post = {
						authorName : msg['feed'][index]['authorName'],
						initPosrID : msg['feed'][index]['initPosrID'],
						likesNum : msg['feed'][index]['likesNum'],
						imageLink : msg['feed'][index]['imageLink'],
						postID: msg['feed'][index]['postID'],
						commentsNum : msg['feed'][index]['commentsNum'],
						text : msg['feed'][index]['text'],
						time : msg['feed'][index]['time'],
						viewNum : msg['feed'][index]['viewNum']};
			console.log(post)
			allPosts = [...allPosts, post];
		}
		for (var i:number = numberOfLoadedPosts; i < numberOfLoadedPosts+10; i++) {
			if(allPosts.length > i){
				posts = [...posts, allPosts[i],];
			}
		}
		numberOfLoadedPosts += 10;
	});

	
	
	
	
	
	
	
	
	
	
	
	
	
	
	let editMode: boolean = false;
	let profileName: HTMLSpanElement;
	let profileDescription: HTMLSpanElement;
	let listElement: HTMLElement;
	let items: string[] = ["Elon Musk", "Elon Musk", "Elon Musk", "Elon Musk", "Elon Musk"];

	let newPost: HTMLSpanElement;

	let temp1: string =
		"Elon Musk's Twitter profile is a reflection of his eclectic personality, his bold ideas, and his vision for the future of technology. At the top of his profile, you'll find a picture of his face, which is often accompanied by a witty or provocative comment.";
	let temp2: string = 'Elon Musk';

	let ownerOfProfile: boolean = true;

	function postPost() {
		items = [`${newPost.innerText}`, ...items];
	}

	function loadMore() {
		for (var i:number = numberOfLoadedPosts; i < numberOfLoadedPosts+10; i++) {
			if(allPosts.length > i){
				posts = [...posts, allPosts[i],];
			}
		}
		numberOfLoadedPosts += 10;
	}

	function editProfile() {
		editMode = !editMode;
	}

	function saveProfile() {
		editMode = !editMode;
	}
</script>

<svelte:head>
	<title>Username</title>
	<meta name="description" content="Username" />
</svelte:head>

<div id="top-container">
	{#if ownerOfProfile}
		{#if !editMode}
			<div id="button-wrapper">
				<button style="color:red; margin:5px 15px 5px 5px;" on:click={editProfile}>Edit</button>
			</div>
		{/if}
		{#if editMode}
			<div id="button-wrapper">
				<button style="color:yellowgreen; margin:5px 15px 5px 5px;" on:click={saveProfile}
					>Save</button>
			</div>
		{/if}
	{/if}
	<div id="post-author-photo" style="margin-top:30px;">
		<img id="photo" src={image_src} alt="profile avatar" style="width:100%;" />
	</div>

	{#if editMode}
		<span
			bind:this={profileName}
			style="width:100px; min-height: 10px;
line-height: 20px; padding:5px 5px 5px 5px;"
			class="textarea"
			role="textbox"
			contenteditable>{temp2}</span
		>
	{/if}
	{#if !editMode}
		<span>{temp2}</span>
	{/if}

	<a href="/{alias_from_url}">
		<span>@{alias_from_url}</span>
	</a>

	{#if editMode}
		<br />
		<span bind:this={profileDescription} class="textarea" role="textbox" contenteditable
			>{temp1}</span>
		<br />
	{/if}
	{#if !editMode}
		<div id="profile-text">{temp1}</div>
	{/if}
</div>

{#if ownerOfProfile}
	<div id="post">
		<div id="post-content-wrapper">
			<div id="comment-wrapper">
				<span bind:this={newPost} class="textarea" role="textbox" contenteditable />
				<div id="button-wrapper">
					<button on:click={postPost}>Post</button>
				</div>
			</div>
		</div>
	</div>
{/if}

<div bind:this={listElement}>
	{#each posts as post}
		<Post authorName={post['authorName']}  authorImageSrc={post['imageLink']} postText={post['text']} numberOfViews={post['viewNum']} dateOfPost={post['time']} numberOfLikes={post['likesNum']} numberOfComments={post['commentsNum']}/>
	{/each}
</div>

<div id="button-wrapper-load">
	<button on:click={loadMore}>Load more</button>
</div>

<style>
	#post {
		box-shadow: rgba(50, 50, 93, 0.1) 0px -10px 100px -20px, rgba(0, 0, 0, 0.07) 0px 30px 60px 10px;
		margin-top: 15px;
		margin-bottom: 15px;
		width: 600px;

		background-color: white;
		border-radius: 10px;
	}
	#post-content-wrapper {
		padding-left: 30px;
		padding-right: 30px;
		padding-top: 10px;
		padding-bottom: 10px;
	}
	#comment-wrapper {
		margin-top: 10px;
	}
	button {
		font-size: medium;
		border: medium none;
		background-image: none;
		background: transparent;
		background-color: transparent;
		color: blue;
		cursor: pointer;
	}
	#button-wrapper {
		margin-left: auto;
		margin-right: 0;
		inline-size: max-content;
		text-align: left;
		padding: 10px 0px 0px 0px;
	}
	#button-wrapper-load {
		inline-size: max-content;
		text-align: left;
		padding: 10px 0px 0px 0px;
	}
	.textarea {
		display: block;
		width: 520px;
		overflow: hidden;
		resize: both;
		min-height: 20px;
		line-height: 25px;
		background: #f1f1f1;
		border: none;
		border-radius: 10px;
		padding-left: 10px;
		padding-right: 10px;
		padding-top: 10px;
		padding-bottom: 10px;
	}

	.textarea[contenteditable]:empty::before {
		content: 'Write what you think...';
		color: gray;
	}

	#profile-text {
		margin: 20px 140px 20px 140px;
		text-indent: 30px;
	}
	#top-container {
		margin-top: 30px;
		display: flex;
		flex-direction: column;
		align-items: center;
		border-radius: 10px;
		width: 600px;
		overflow: hidden;
		box-shadow: rgba(0, 0, 0, 0.07) 0px -100px 100px -40px;
		background-image: linear-gradient(
			to bottom,
			rgb(255, 255, 255) 0%,
			rgba(255, 255, 255, 0) 100%
		); /* Set a linear-gradient background with initial opacity of 1 at the top and 0 at the bottom */
		background-size: 100% 100%; /* Set the background size to cover the entire div element */
	}

	#post-author-photo {
		width: 88px;
		height: 88px;
		margin-top: 3px;
		margin-bottom: 3px;
		border-radius: 30px;
		overflow: hidden;
	}
</style>
