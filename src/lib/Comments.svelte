<script lang="ts">
    import Comment from '$lib/Comment.svelte';
    import { page } from '$app/stores';
    import { io } from 'socket.io-client';
	import { API_URL } from '$lib/env';
	const socket = io(API_URL);
	let alias_from_url = $page.params.username;
    let tweetId_from_url = $page.params.tweeetId;
    // <!-- export let authorPhotoLink: string;
    //         export let authorName: string;
    //         export let commentText: string;
    //         export let dateOfComment: string; -->

    interface Comment{
        authorPhotoLink: string;
        authorName: string;
        commentText: string;
        dateOfComment: string; 
    }

    let commentText:string;
    let items1:string[] = ["Good job man!", "Keep striving!", "Good luck!","Fuck FWD", "Here was Egor"];
    let comments:Comment[] = []
    let allComments:Comment[] = []
	let numberOfLoadedComments:number = 0;
    let listElement:HTMLDivElement;
    let newComment:HTMLSpanElement;

    function postComment() {
		

    }

    socket.emit('get-post-comments', {'postID': +tweetId_from_url})

    socket.on('get-post-comments-result', (msg) => {
        console.log(msg);
		console.log(msg['feed']);
		for (let index in msg['feed']) {
			let comment: Comment = {
                                'authorPhotoLink' : msg['feed'][index]['avatar'],
                                'authorName' : msg['feed'][index]['authorName'],
                                'commentText' : msg['feed'][index]['text'],
                                'dateOfComment' : msg['feed'][index]['time']};
			console.log("ВАШ ПОСТ АЙДИ СЕР:");
            console.log("")

			allComments = [...allComments, comment];
		}
		for (var i:number = numberOfLoadedComments; i < numberOfLoadedComments+10; i++) {
			if(allComments.length > i){
				comments = [...comments, allComments[i],];
			}
		}
		numberOfLoadedComments += 10;
    });    

    function loadMore() {
		socket.emit('get-post-comments', {'postID': +tweetId_from_url})
	}
</script>

<div id="post">
    
    
    <div id="post-content-wrapper">
        
        <div id="comment-wrapper">
            <span bind:this={newComment} class="textarea" role="textbox" contenteditable></span>
            <div id="button-wrapper">
                <button on:click={postComment}>Post</button>
            </div>
        </div>
        
        <div bind:this={listElement} >
            {#each comments as comment}
                <!-- <Comment authorPhotoLink={} authorName={} commentText={} dateOfComment={}/> -->
            {/each}
        </div>
        
        <div id="button-wrapper">
            <button on:click={loadMore}>Load more</button>
        </div>
        
    </div>
</div>




<style>
#comment-wrapper{
    margin-top:10px;
}
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
    padding-left:10px;
    padding-right:10px;
    padding-top:10px;
    padding-bottom:10px;
}

.textarea[contenteditable]:empty::before {
  content: "Write what you think...";
  color: gray;
}
p strong {
  display: block;
}
    .width-machine {
  /*   Sort of a magic number to add extra space for number spinner */
  padding: 0 1rem;
}
.field{
    padding-top:12px;
    padding-bottom: 12px;
    
}


#photo-wrap{
    display: flex;
    flex-direction: row;
    justify-content: start;
}
#photo{
    width:100%;
    height:100%;
}
#views-wrap{
    width:200px;
    margin-top:7px;
    margin-left: auto;
    margin-right: 0em;
    margin-bottom: 0px;
}
#views{
    color: #363636;
    font-size: 16px;
    text-align: right;
}
#post{
    box-shadow: rgba(50, 50, 93, 0.10) 0px -10px 100px -20px, rgba(0, 0, 0, 0.07) 0px 30px 60px 10px;
    margin-top:15px;
    margin-bottom:15px;
    width:600px;
    
    background-color: white;
    border-radius: 10px;
}
#post-content-wrapper{
    padding-left: 30px;
    padding-right: 30px;
    padding-top: 10px;
    padding-bottom:10px;
}
#post-author{
    font-size: 20px;
    padding-top: 15px;
    padding-bottom: 15px;
    margin-left: 10px;
}
#post-author-photo{
    width:44px;
    height:44px;
    margin-top: 3px;
    margin-bottom: 3px;
    border-radius: 30px;
    background-color: red;
    overflow: hidden;
}
#post-text{
    
}
#activities{
    display: flex;
    flex-direction: row;
}
.activity-text{
    color: blue;
    padding-top:15px;
    margin-right:50px;
    padding-bottom:10px;
}
</style>