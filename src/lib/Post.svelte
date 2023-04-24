<script lang="ts">
	export let authorName: string;
    export let authorImageSrc: string;
    export let postText: string;
	export let numberOfViews: number;
    export let dateOfPost: string;
    export let numberOfLikes: number;
    export let numberOfComments: number;
    

    let ownerOfPost:boolean = true;
    let postIsLiked:boolean = true;
    let editMode:boolean = false;
    let deletedPost:boolean = false;

    let newText : HTMLSpanElement;

    function likePost(){
        postIsLiked = !postIsLiked;
        console.log("Liked");
    }

    function editPost(){
        editMode = !editMode;
        if(!editMode){
            postText = newText.innerText;
        }
    }

    function sharePost(){
        console.log("Share post");
    }

    function commentPost(){
        console.log("Comment post");
    }

    function deletePost(){
        deletedPost = true;
        console.log("Delete post");
    }

    //image_src = "https://cdn-icons-png.flaticon.com/512/168/168732.png"
    //text = "Немецкий концерн Rheinmetall откроет в Румынии, рядом с украинской границей, ремонтный и логистический хаб для техобслуживания вооружений, поставляемых Украине, в том числе, немецких танков Leopard и британских Challenger. Об этом сообщает Reuters со ссылкой на саму компанию";
    //author = "DW на русском";
</script>

{#if !deletedPost}
<div id="post">
    
    
    <div id="post-content-wrapper">
        <div id="photo-wrap">
            <div id="post-author-photo">
                <img id="photo" src={authorImageSrc} alt="profile avatar" />
            </div>
            <div id="post-author">
                <b>{authorName}</b>
            </div>
        </div>

        {#if !editMode}
        <div id="post-text">
            {postText}
        </div>
        {/if}
        {#if editMode}
        <div id="comment-wrapper">
            <span bind:this={newText} class="textarea" role="textbox" contenteditable>{postText}</span>
        </div>
        {/if}
        


        <div id="views-wrap">
            <div id="views">
                {dateOfPost}
            </div>
        </div>

        <div id="activities">
            {#if !postIsLiked}
            <div on:click={likePost} on:keypress={likePost} class="activity-text" id="likes">
                {numberOfLikes} ❤️
            </div>
            {/if}
            {#if postIsLiked}
            <div on:click={likePost} on:keypress={likePost} class="activity-text-liked">
                {numberOfLikes} ❤️
            </div>
            {/if}
            <div on:click={commentPost} on:keypress={commentPost} class="activity-text" id="comments">
                {numberOfComments} Comments
            </div>
            <div on:click={sharePost} on:keypress={sharePost} class="activity-text" id="share">
                Share
            </div>
            {#if ownerOfPost}
            {#if !editMode}
            <div on:click={editPost} on:keypress={editPost} class="activity-text" id="edit">
                Edit
            </div>
            {/if}
            {#if editMode}
            <div on:click={editPost} on:keypress={editPost} class="activity-text-edit" id="edit" style="color:yellowgreen;">
                Save
            </div>
            {/if}

            <div on:click={deletePost} on:keypress={deletePost} class="activity-text" id="delete">
                Delete
            </div>
            {/if}
        </div>
        
    </div>
</div>

{/if}


<style>
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
#edit{
    color:red;
}
#delete{
    color:red;
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
    user-select: none;
        -moz-user-select: none;
        -khtml-user-select: none;
        -webkit-user-select: none;
        -o-user-select: none;
    color: blue;
    padding-top:10px;
    padding-bottom:10px;
    
    margin-top:5px;
    margin-bottom:5px;

    margin-right:30px;
    padding-left:10px;
    padding-right: 10px;
    height: 20px;
}
.activity-text-edit{
    user-select: none;
    -moz-user-select: none;
    -khtml-user-select: none;
    -webkit-user-select: none;
    -o-user-select: none;
    
    color: green;
    padding-top:10px;
    padding-bottom:10px;
    
    margin-top:5px;
    margin-bottom:5px;

    margin-right:30px;
    padding-left:10px;
    padding-right: 10px;
    height: 20px;
}
.activity-text-liked{
    user-select: none;
        -moz-user-select: none;
        -khtml-user-select: none;
        -webkit-user-select: none;
        -o-user-select: none;
    color: white;
    background-color: blue;
    border-radius: 10px;
    
    padding-top:10px;
    padding-bottom:10px;
    
    margin-top:5px;
    margin-bottom:5px;

    margin-right:30px;
    padding-left:10px;
    padding-right: 10px;
    height: 20px;
}
</style>