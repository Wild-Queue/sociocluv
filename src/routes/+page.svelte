<script lang="ts">
    import RegisterForm from '$lib/RegisterForm.svelte';
    import LoginForm from '$lib/LoginForm.svelte';
    import { onMount } from 'svelte';
    
    let needRegistration:boolean = false;

    onMount(() => {
		sessionStorage.setItem('authorized', 'false');
        sessionStorage.setItem('userid', '');
	});
</script>


<div id="form-wrap">
    {#if needRegistration}
    <RegisterForm bind:register={needRegistration}/>
    {/if}
    {#if !needRegistration}
    <LoginForm bind:login={needRegistration} />
    {/if}
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

