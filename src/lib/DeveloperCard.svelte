<script lang="ts">
	export let imgSrc: string;
	export let name: string;
	export let role: string;
</script>

<div id="content">
	<div><img src={imgSrc} alt="developer" /></div>
	<div id="name">{name}</div>
	<div id="role">{role}</div>
</div>

<style>
	img {
		width: 200px;
		border-radius: 30px;
	}
    #content{
        display: flex;
        flex-direction: column;
        margin-bottom:10px;
        margin-top:10px;
    }
    #name{
        font-size: 20px;
        margin:auto;
    }
    #role{
        margin:auto;
    }
</style>
