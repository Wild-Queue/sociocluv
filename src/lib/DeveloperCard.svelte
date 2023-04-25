<script lang='ts'>
    export let imgSrc:string;
    export let name:string;
    export let role:string;
</script>

<div>
<img src={imgSrc} alt="developer"/>
<p>{name}</p>
<p>{role}</p>
</div>

<style>
img{
    width:300px;
}
</style>