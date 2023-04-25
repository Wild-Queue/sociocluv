<script lang="ts">
	export let imgSrc: string;
	export let name: string;
	export let role: string;
</script>

<div>
	<img src={imgSrc} alt="developer" />
	<div style="margin:auto;">{name}</div>
	<div style="margin:auto;">{role}</div>
</div>

<style>
	img {
		width: 300px;
		border-radius: 30px;
	}
</style>
