<script lang='ts'>
import DeveloperCard from "$lib/DeveloperCard.svelte";

</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="home" />
</svelte:head>
<div id="content-flex">
	<DeveloperCard imgSrc="https://imgpile.com/images/h3SzLS.md.png" name="Vladislav Spigin" role="DevOps+Front"/>
	<DeveloperCard imgSrc="https://imgpile.com/images/h3Sclx.png" name="Egor Shalagin" role="Backend+Front"/>
	<DeveloperCard imgSrc="https://imgpile.com/images/h3SPXP.png" name="Arseniy Rubtsov" role="Design+Front"/>
</div>
<br>
<p>Sociocluv is a social networking platform that allows users to connect with friends and family, share their thoughts, and engage in meaningful conversations.</p>
<img src="https://www.allaboutbirds.org/news/wp-content/uploads/2020/07/STanager-Shapiro-ML.jpg" alt="bird">
<style>
#content-flex{
	display: flex;
	flex-direction: column;	
}
img{
	width:500px;
	border-radius: 20px;
}
</style>