<script lang="ts">
	let correctUsername = 'ManikSharma';
	let correctPassword = 'Manik@123';

	let enteredUsername = $state('');
	let enteredPassword = $state('');

	function handleLogin() {
		if (enteredUsername === correctUsername && enteredPassword === correctPassword) {
			alert('Login successful!');
		} else {
			alert('Invalid username or password.');
		}
	}
</script>

<main class="min-h-screen flex flex-col items-center justify-center text-center p-4">
	<form onsubmit={handleLogin}>
		<label>
			Username:
			<input bind:value={enteredUsername} required />
		</label>
		<br />
		<label>
			Password:
			<input type="password" bind:value={enteredPassword} required />
		</label>
		<br />
		<button type="submit">Login</button>
	</form>
</main>
