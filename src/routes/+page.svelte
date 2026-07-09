<script lang="ts">
	import Particles from './particles.svelte';

	let correctUsername = 'testuser';
	let correctPassword = '1234';

	let registeredUsername = '';
	let registeredPassword = '';

	let label = $state('');

	let chosen = $state('login');

	let enteredUsername = $state('');
	let enteredPassword = $state('');

	function handleLogin() {
		if (enteredUsername === correctUsername && enteredPassword === correctPassword) {
			label = 'Login successful!';
		} else if (enteredUsername === registeredUsername && enteredPassword === registeredPassword) {
			label = 'Login successful!';
		} else {
			label = 'Invalid username or password.';
		}
	}

	function handleRegister() {
		registeredUsername = enteredUsername;
		registeredPassword = enteredPassword;
		label = 'Registration successful!';
	}
</script>

<main
	class="z-10 min-h-screen flex flex-col items-center justify-center text-center p-4 bg-[#6666ff] text-white"
>
	<p class="mb-4 text-4xl font-bold font-[AQUIRE]">METRO NEXUS</p>
	<div class="flex gap-2"></div>
	{#if chosen === 'login'}
		<form
			onsubmit={handleLogin}
			class="bg-white/10 border border-white/10 p-10 rounded-xl backdrop-blur-2xl text-black"
		>
			<input bind:value={enteredUsername} required class="button2" placeholder="Phone/Email" />

			<br />
			<input
				type="password"
				bind:value={enteredPassword}
				required
				class="button2 mt-2 shadow-xl"
				placeholder="Password"
			/>
			<br />
			<p class="mt-2 text-xs">
				Or, alternatively, <button onclick={() => (chosen = 'register')} class="underline">
					Register
				</button>
			</p>
			<button type="button" onclick={handleLogin} class="button3 mt-2">Login</button>
			<p class="mt-2">{label}</p>
		</form>
	{/if}
	{#if chosen === 'register'}
		<form class="bg-white/10 border border-white/10 p-10 rounded-xl backdrop-blur-2xl text-black">
			<input bind:value={enteredUsername} required class="button2" placeholder="Phone/Email" />
			<br />
			<input
				type="password"
				bind:value={enteredPassword}
				required
				class="button2 mt-2 shadow-xl"
				placeholder="Password"
			/>
			<br />
			<p class="mt-2 text-xs">
				Or, alternatively, <button onclick={() => (chosen = 'login')} class="underline">
					Login
				</button>
			</p>
			<button type="button" onclick={handleRegister} class="button3 mt-2">Register</button>
			<p class="mt-2">{label}</p>
		</form>
	{/if}
</main>
