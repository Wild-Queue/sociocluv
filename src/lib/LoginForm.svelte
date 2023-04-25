<script lang="ts">
	import { io } from 'socket.io-client';
	import { API_URL } from '$lib/env';
	const socket = io(API_URL);
	let username: string = '';
	let password: string = '';
	let errorMessage: string = 'Handle value of errorMessage!';

	export let login: boolean;

	function loginUser() {
		console.log('LoginFunction');
		if (username == '') {
			errorMessage = 'Empty username!';
		} else if (password == '') {
			errorMessage = 'Empty password!';
		} else {
			errorMessage = '';
			socket.emit('sign-in', { login: username, password: password });
		}
		console.log(username);
		console.log(password);

		//Wrong password or username

		//Existing username! Username should be unique!
		socket.on('sign-in-result', (msg) => {
			if (msg['result'] == false) {
				errorMessage = 'Incorrect password or login!';
			} else {
				console.log('Login success');
				let userID: number = msg['userID'];

				sessionStorage.setItem('authorized', 'true');
				sessionStorage.setItem('userid', msg['userID'].toString());
				window.location.href = '/home';
			}
		});
	}

	function switchToRegistration() {
		console.log('CreateAccount');
		login = true;
	}
</script>

<!-- Имя, пароль, почта?, дата рождения-->
<div id="registration">
	<form>
		<div id="content-wrapper">
			<div id="registration-text">Login</div>
			<div class="field">
				<input type="username" bind:value={username} id="username" placeholder="Username" />
			</div>
			<div class="field">
				<input type="password" bind:value={password} id="password" placeholder="Password" />
			</div>
			<div id="error-text">{errorMessage}</div>
			<div>
				Don't have an account?
				<button on:click={switchToRegistration}>Create account</button>
				<div id="button-wrapper">
					<button on:click={loginUser}>Log In</button>
				</div>
			</div>
		</div>
	</form>
</div>

<style>
	#error-text {
		color: red;
	}
	#registration-text {
		font-size: 31px;
		font-weight: bold;
		padding-top: 40px;
		padding-bottom: 10px;
	}
	#content-wrapper {
		padding: 0px 80px 10px 80px;
	}
	button {
		margin-left: 0px;
		padding-left: 0px;
	}
	#button-wrapper {
		margin-left: auto;
		margin-right: 0;
		inline-size: max-content;
		text-align: left;
		padding: 10px 0px 15px 0px;
	}
	.field {
		padding-top: 12px;
		padding-bottom: 12px;
	}
	input {
		height: 64px;
		border: none;
		background: #f1f1f1;
		width: 400px;
		padding: 0px;
		border-radius: 10px;
		font-size: 15px;
		padding-left: 20px;
		padding-right: 20px;
	}

	input:focus {
		background-color: #ddd;
		outline: none;
	}
	#form-wrap {
		display: block;
	}
	label {
		margin-bottom: 10%;
	}
	button {
		font-size: medium;
		border: medium none;
		background-image: none;
		background: transparent;
		background-color: transparent;
		color: blue;
		cursor: pointer;
	}
	#registration {
		width: 600px;
		background-color: white;
		border-radius: 5%;
		box-shadow: rgba(50, 50, 93, 0.15) 0px -10px 100px -20px, rgba(0, 0, 0, 0.07) 0px 30px 60px 10px;
		margin-top: 30px;
		margin-bottom: 30px;
	}
</style>
