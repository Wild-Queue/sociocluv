<script lang="ts">
	let username: string;
	let password: string;
	let email: string;

	function SignUp(e: SubmitEvent) {
		console.log(username, password, email);
		username = '';
		password = '';
		email = '';
	}
</script>

<!-- Имя, пароль, почта?, дата рождения-->
<div id="registration">
	<form on:submit|preventDefault={SignUp}>
		<div id="content-wrapper">
			<div id=registration-text>Registration</div>
			<div class="field">
				<input type="username" bind:value={username} id="username" placeholder="Username" />
			</div>
			<div class="field">
				<input type="email" bind:value={email} id="email" placeholder="Email" />
			</div>
			<div class="field">
				<input type="password" bind:value={password} id="password" placeholder="Password" />
			</div>
			<div id="button-wrapper">
				<button type="submit"> Sign Up</button>
			</div>
		</div>
	</form>
</div>

<style>
	#registration-text{
		font-size: 31px;
		font-weight: bold;
		padding-top:40px;
		padding-bottom:10px;
	}
	#content-wrapper{
		padding: 0px 80px 10px 80px;	 
	}
	#button-wrapper{
		margin-left: auto; 
		margin-right: 0;
		inline-size: max-content;
		text-align: right;
		padding: 20px 0px 20px 0px;
		
	}
	.field{
		padding-top:12px;
		padding-bottom: 12px;
		
	}
	input {
		height: 64px;
		border: none;
		background: #f1f1f1;
		width:400px;
		padding:0px;
		border-radius: 10px;
		font-size:15px;
		padding-left:20px;
		padding-right:20px;

	}

	input:focus{
		background-color: #ddd;
		outline: none;
	}
	#form-wrap {
		display: block;
	}
	label{
		margin-bottom: 10%;
	}
	button {
		font-size:medium;
		border: medium none;
		background-image: none;
		background: transparent;
		background-color: transparent;
		color: blue;
		cursor: pointer;
	}
	#registration {
		width:600px;
		background-color: white;
		border-radius: 5%;
		box-shadow: rgba(50, 50, 93, 0.15) 0px -10px 100px -20px, rgba(0, 0, 0, 0.07) 0px 30px 60px 10px;
		margin-top:30px;
		margin-bottom:30px;
	}
</style>
