<script lang="ts">
	import Comment from '$lib/Comment.svelte';
	import { page } from '$app/stores';
	import { io } from 'socket.io-client';
	import { API_URL } from '$lib/env';


	const socket = io(API_URL);
	let alias_from_url:string = $page.params.username;
	let tweetId_from_url:string = $page.params.tweeetId;

	interface Comment {
		authorPhotoLink: string;
		authorName: string;
		commentText: string;
		dateOfComment: string;
	}

	let commentText: string;
	let items1: string[] = [
		'Good job man!',
		'Keep striving!',
		'Good luck!',
		'Fuck FWD',
		'Here was Egor'
	];
	let comments: Comment[] = [];
	let allComments: Comment[] = [];
	let numberOfLoadedComments: number = 0;

	let listElement: HTMLDivElement;
	let newComment: HTMLSpanElement;

    function postComment() {
		if (newComment.innerText != '') {
			commentText = newComment.innerText;
			numberOfLoadedComments = 0;

			let comment:Comment = {
				authorPhotoLink: "https://images.theconversation.com/files/508626/original/file-20230207-21-k6uwib.jpg?ixlib=rb-1.1.0&q=45&auto=format&w=1200&h=1200.0&fit=crop",
                authorName: alias_from_url,
                commentText: commentText,
                dateOfComment: "",
			};

			console.log(commentText);
			socket.emit('make-comment', {
				authorAlias : alias_from_url.toString(),
                postID : parseInt(tweetId_from_url),
                text : commentText,
			});
			comments = [comment, ...comments];
		}
		commentText = '';
	}

	socket.emit('get-post-comments', { postID: parseInt(tweetId_from_url) });

	socket.on('get-post-comments-result', (msg) => {
		console.log(msg);
		console.log(msg['feed']);
		for (let index in msg['feed']) {
			let comment: Comment = {
				authorPhotoLink: msg['feed'][index]['avatar'],
				authorName: msg['feed'][index]['authorName'],
				commentText: msg['feed'][index]['text'],
				dateOfComment: msg['feed'][index]['time']
			};
			console.log('ВАШ ПОСТ АЙДИ СЕР:');
			console.log(comment);

			allComments = [...allComments, comment];
		}
		for (var i: number = numberOfLoadedComments; i < numberOfLoadedComments + 10; i++) {
			if (allComments.length > i) {
				comments = [...comments, allComments[i]];
			}
		}
		numberOfLoadedComments += 10;
	});

	function loadMore() {
        for (var i: number = numberOfLoadedComments; i < numberOfLoadedComments + 10; i++) {
			if (allComments.length > i) {
				comments = [...comments, allComments[i]];
			}
		}
		numberOfLoadedComments += 10;
	}
</script>

<div id="post">
	<div id="post-content-wrapper">
		<div id="comment-wrapper">
			<span bind:this={newComment} class="textarea" role="textbox" contenteditable />
			<div id="button-wrapper">
				<button on:click={postComment}>Post</button>
			</div>
		</div>

		<div bind:this={listElement}>
			{#each comments as comment}
				<Comment authorPhotoLink={comment["authorPhotoLink"]} authorName={comment["authorName"]} commentText={comment["commentText"]} dateOfComment={comment["dateOfComment"]}/>
			{/each}
		</div>

		<div id="button-wrapper">
			<button on:click={loadMore}>Load more</button>
		</div>
	</div>
</div>

<style>
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
</style>
