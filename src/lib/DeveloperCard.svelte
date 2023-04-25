<script lang="ts">
	export let imgSrc: string;
	export let name: string;
	export let role: string;
</script>

<div id="content">
	<img src={imgSrc} alt="developer" />
	<div>{name}</div>
	<div>{role}</div>
</div>

<style>
	img {
		width: 300px;
		border-radius: 30px;
	}
    #content{
        display: flex;
        flex-direction: column;
    }
</style>
