<script lang='ts'>
    import Post from "$lib/Post.svelte";
    import Comments from "$lib/Comments.svelte";
    import { page } from '$app/stores';
	import { io } from 'socket.io-client';
	let alias_from_url = $page.params.username;
    let tweetId_from_url = $page.params.tweeetId;
	const socket = io('http://localhost:5050/');
    
    let postExist:boolean = true;

    interface Post{
		authorID : number;
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
    socket.emit('get-single-post', {postID: +tweetId_from_url});
    
    let post:Post = {authorID : 0,
						authorName : '',
						initPosrID : 0,
						likesNum : 0,
						imageLink : '',
						postID: 0,
						commentsNum : 0,
						text : '',
						time : '',
						viewNum : 0};
    
    socket.on('get-post-comments-result', (msg) => {
        if (msg['result'] === true){
            post = {//msg['postData']
                'authorID' : msg['postData']['authorID'],
                'authorName' : msg['postData']['authorName'], 
                'initPosrID': msg['postData']['initPosrID'],
                'likesNum': msg['postData']['likesNum'],
                'postID': msg['postData']['postID'],
                'commentsNum': msg['postData']['commentsNum'],
                'imageLink' : msg['postData']['imageLink'],
                'text': msg['postData']['text'],
                'time': msg['postData']['time'],
                'viewNum': msg['postData']['viewNum']
            };
            postExist = true;
        }else if (msg['result'] === false){
            console.log('Post is not found')
            postExist = false;
        }
    });

</script>


<svelte:head>
	<title>Single Tweet</title>
	<meta name="description" content="tweet" />
</svelte:head>

{#if postExist}
<div>
    <!--<Post author="Arseniy"/>-->
    <!--<span>Username: {alias_from_url}</span>-->
    <!--<span>TweetId: {tweetId_from_url}</span>-->
    <Post authorName={post['authorName']}  authorImageSrc={post['imageLink']} postText={post['text']} numberOfViews={post['viewNum']} dateOfPost={post['time']} numberOfLikes={post['likesNum']} numberOfComments={post['commentsNum']} userId={post['authorID']} postId={post['postID']}/>
    <Comments/>
</div>
{/if}
{#if !postExist}
<p>Post not found!</p>
{/if}