<script lang="ts">
	import { error } from "@sveltejs/kit";
	import { io } from 'socket.io-client';
	import { redirect } from '@sveltejs/kit';


	const socket = io('http://localhost:5050/');

	let username: string = "";
	let password: string = "";
	let email: string = "";
	let errorMessage:string = "Handle value of errorMessage!";
	let authorized:boolean = false;

	export let register:boolean;

	function signUpUser() {
		console.log("SignUpUser");
		if(username == ""){
			errorMessage = "Empty username!";
		}else if(email == ""){
			errorMessage = "Empty email!";
		}else if(password == ""){
			errorMessage = "Empty password!";
		}else if(username.length < 6){
			errorMessage = "Username length should be more than 6 symbols!";
		}else if(!email.includes('@') || !email.includes('.')){
			errorMessage = "Incorrect email type!";
		}else if(password.length < 10){
			errorMessage = "Password length should be more than 10 symbols!";
		}else if(!(/[a-z]/.test(password)) || !(/[A-Z]/.test(password)) || !(/[0-9]/.test(password))){
			errorMessage = "Too simple password! Password should contain at least one [A-Z], [a-z] and [0-9].";
		}else{
			errorMessage = "";
			socket.emit('sign-up', {login: username, password: password, email: email})
		}
		
		
		//Existing username! Username should be unique!
		socket.on('sign-up-result', (msg) => {
			if (msg['result'] === false && msg['userID'] === -1){
				errorMessage = "User with such login already exist!";
			}
			else if (msg['result'] === false && msg['userID'] === -1){
				errorMessage = "Insert into database went wrong, try again";
			}
			else{
				console.log("Registration success");
				let userID:number = msg['userID']

				sessionStorage.setItem('authorized', 'true');
				sessionStorage.setItem('userid', msg['userID'].ToString());
				window.location.href = '/home';
			}
		});errorMessage
	}

	

	

	
	function switchToLogin() {
		console.log("CreateAccount");
		register = false;
    }
</script>
{#if !authorized}
<!-- Имя, пароль, почта?, дата рождения-->
<div id="registration">
	<form>
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
			<div id="error-text">{errorMessage}</div>
			<div>
				Already have an account?
				<button on:click={switchToLogin}>Log In</button>
				<div id="button-wrapper">
					<button on:click={signUpUser}>Sign Up</button>
				</div>
			</div>
		</div>
	</form>
</div>
{/if}
<style>
	#error-text{
		color:red;
	}
	#registration-text{
		font-size: 31px;
		font-weight: bold;
		padding-top:40px;
		padding-bottom:10px;
	}
	#content-wrapper{
		padding: 0px 80px 10px 80px;	 
	}
	button{
		margin-left:0px;
		padding-left:0px;
	}
	#button-wrapper{
		margin-left: auto; 
		margin-right: 0;
		inline-size: max-content;
		text-align: left;
		padding: 10px 0px 15px 0px;
		
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
