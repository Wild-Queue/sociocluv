<script lang="ts">
	import DeveloperCard from '$lib/DeveloperCard.svelte';
</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="home" />
</svelte:head>
<div id="content-flex">
	<DeveloperCard
		imgSrc="https://www.australiangeographic.com.au/wp-content/uploads/2020/12/E1R8HC-900x643.jpg"
		name="Vladislav Spigin"
		role="DevOps + Front"
	/>
	<DeveloperCard
		imgSrc="https://media.npr.org/assets/img/2021/11/05/ap21309626616879_wide-15b2fb050f8a01806c5e3c598df7c01d8d756fa4-s1400-c100.jpg"
		name="Egor Shalagin"
		role="Backend + Front"
	/>
	<DeveloperCard
		imgSrc="https://media.newyorker.com/photos/5a95a5b13d9089123c9fdb7e/1:1/w_3289,h_3289,c_limit/Petrusich-Dont-Mess-with-the-Birds.jpg"
		name="Arseniy Rubtsov"
		role="Design + Front"
	/>
</div>
<br />
<div id="description">
	Sociocluv is a social networking platform that allows users to connect with friends and family,
	share their thoughts, and engage in meaningful conversations.
</div>
<img
	src="https://www.allaboutbirds.org/news/wp-content/uploads/2020/07/STanager-Shapiro-ML.jpg"
	alt="bird"
/>

<style>
	#description{
		font-size:20px;
		text-indent: 30px;
		margin:auto; 
		width:300px;
		margin-top:20px;
		margin-bottom:20px;
	}
	#content-flex {
		display: flex;
		flex-direction: column;
	}
	img {
		width: 300px;
		border-radius: 20px;
	}
</style>
