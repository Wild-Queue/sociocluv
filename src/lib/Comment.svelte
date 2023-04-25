<script lang="ts">
	export let authorPhotoLink: string;
	export let authorName: string;
	export let commentText: string;
	export let dateOfComment: string;
</script>

<div id="post">
	<div id="post-content-wrapper">
		<div id="photo-wrap">
			<div id="post-author-photo">
				<img id="photo" src={authorPhotoLink} alt="profile avatar" />
			</div>
			<div id="post-author">
				<b>{authorName}</b>
			</div>
		</div>

		<div id="post-text">
			{commentText}
		</div>

		<div id="views-wrap">
			<div id="views">
				{dateOfComment}
			</div>
		</div>
	</div>
</div>

<style>
	#photo-wrap {
		display: flex;
		flex-direction: row;
		justify-content: start;
	}
	#photo {
		width: 100%;
		height: 100%;
	}
	#views-wrap {
		width: 200px;
		margin-top: 7px;
		margin-left: auto;
		margin-right: 0em;
		margin-bottom: 0px;
	}
	#views {
		color: #363636;
		font-size: 16px;
		text-align: right;
	}
	#post {
		box-shadow: rgba(50, 50, 93, 0.1) 0px -10px 100px -20px, rgba(0, 0, 0, 0.07) 0px 30px 60px 10px;
		margin-top: 15px;
		margin-bottom: 15px;
		width: 540px;

		background-color: white;
		border-radius: 10px;
	}
	#post-content-wrapper {
		padding-left: 30px;
		padding-right: 30px;
		padding-top: 10px;
		padding-bottom: 10px;
	}
	#post-author {
		font-size: 16px;
		padding-top: 10px;
		padding-bottom: 15px;
		margin-left: 10px;
	}
	#post-author-photo {
		width: 30px;
		height: 30px;
		margin-top: 3px;
		margin-bottom: 3px;
		border-radius: 30px;
		background-color: red;
		overflow: hidden;
	}
</style>
