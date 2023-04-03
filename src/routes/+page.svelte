<script>
    import Form from '$lib/Form.svelte';
    import Post from '$lib/Post.svelte';
    import Header from "$lib/Header.svelte";
</script>

<Header/>
<div id="holder">
<div id="form-wrap">
    <Form />
</div>
<div id="feed-container">
<div id="post-wrap">
    <Form />
    <Post />
    <Post />
    <Post />
    <Post />
    <Post />
</div>
</div>
</div>

<style>
#feed-container{
    display:flex;
    flex-direction: colums;
}
#post-wrap{

}
#form-wrap{

}
#holder{
    width:100%;
    display: flex;
    flex-direction: row;
    justify-content: space-around;
    background-color: white;
}
</style>

