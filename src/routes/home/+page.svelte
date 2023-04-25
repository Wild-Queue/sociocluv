<script lang="ts">
	import Post from '$lib/Post.svelte';
	import { io } from 'socket.io-client';
	import { onMount, onDestroy } from 'svelte';
	let listElement: HTMLDivElement;

	import { API_URL } from '$lib/env';
	const socket = io(API_URL);

	// let items:string[] = ["Arseniy", "Nikita", "Bob", "Sam", "Kate", "Watter", "Kamble", "Nani","Arseniy", "Nikita", "Bob", "Sam", "Kate", "Watter", "Kamble", "Nani","Arseniy", "Nikita", "Bob", "Sam", "Kate", "Watter", "Kamble", "Nani"];

	// for (let index = 0; index < 20; index++) {
	// 	items = [...items, `${items[index]}`];
	// }
	//Request to database
	interface Post {
		authorID: number;
		authorName: string;
		initPosrID: number;
		likesNum: number;
		postID: number;
		commentsNum: number;
		imageLink: string;
		text: string;
		time: string;
		viewNum: number;
	}

	socket.emit('get-feed', {});

	let allPosts: Post[] = [];
	let posts: Post[] = [];
	let numberOfLoadedPosts: number = 0;

	//Waiting for response
	socket.on('get-feed-result', (msg) => {
		console.log(msg);
		console.log(msg['feed']);
		for (let index in msg['feed']) {
			let post: Post = {
				authorID: msg['feed'][index]['authorID'],
				authorName: msg['feed'][index]['authorName'],
				initPosrID: msg['feed'][index]['initPosrID'],
				likesNum: msg['feed'][index]['likesNum'],
				imageLink: msg['feed'][index]['imageLink'],
				postID: msg['feed'][index]['postID'],
				commentsNum: msg['feed'][index]['commentsNum'],
				text: msg['feed'][index]['text'],
				time: msg['feed'][index]['time'],
				viewNum: msg['feed'][index]['viewNum']
			};
			console.log('ВАШ ПОСТ АЙДИ СЕР:');
			console.log(post.postID);

			allPosts = [...allPosts, post];
		}
		for (var i: number = numberOfLoadedPosts; i < numberOfLoadedPosts + 10; i++) {
			if (allPosts.length > i) {
				posts = [...posts, allPosts[i]];
			}
		}
		numberOfLoadedPosts += 10;
	});

	function loadMore() {
		for (var i: number = numberOfLoadedPosts; i < numberOfLoadedPosts + 10; i++) {
			if (allPosts.length > i) {
				posts = [...posts, allPosts[i]];
			}
		}
		numberOfLoadedPosts += 10;
	}
</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Home page on sociocluv" />
	<meta property="og:title" content="Your home page on sociocluv.">
	<meta property="og:type" content="website">
	<meta property="og:image" content="https://www.allaboutbirds.org/news/wp-content/uploads/2020/07/STanager-Shapiro-ML.jpg">
	<meta property="og:description" content='Home page on sociocluv'>
</svelte:head>

<h1>Explore the world of Sociocluv:</h1>

<div bind:this={listElement}>
	{#each posts as post}
		<Post
			userId={post['authorID']}
			postId={post['postID']}
			authorName={post['authorName']}
			authorImageSrc={post['imageLink']}
			postText={post['text']}
			numberOfViews={post['viewNum']}
			dateOfPost={post['time']}
			numberOfLikes={post['likesNum']}
			numberOfComments={post['commentsNum']}
		/>
	{/each}
</div>

<div id="button-wrapper">
	<button on:click={loadMore}>Load more</button>
</div>

<style>
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
		inline-size: max-content;

		padding: 10px 0px 15px 0px;
	}
</style>
