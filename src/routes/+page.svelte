<script lang="ts">
	import { goto } from '$app/navigation';
	import { onMount } from 'svelte';

	let correctUsername = 'Pranav';
	let correctPassword = '1234';

	let registeredUsername = '';
	let registeredPassword = '';

	let label = $state('');
	let chosen = $state<'login' | 'register'>('login');

	let enteredUsername = $state('');
	let enteredPassword = $state('');

	let isLarge = $state(false);

	onMount(() => {
		const update = () => (isLarge = window.innerWidth >= 768);
		update();
		window.addEventListener('resize', update);
		return () => window.removeEventListener('resize', update);
	});

	async function handleLogin() {
		if (enteredUsername === correctUsername && enteredPassword === correctPassword) {
			label = 'Login successful!';
			document.cookie = 'loggedIn=true; path=/; max-age=31536000';
			document.cookie = `username=${encodeURIComponent(enteredUsername)}; path=/; max-age=31536000`;
			await goto('/account');
		} else if (enteredUsername === registeredUsername && enteredPassword === registeredPassword) {
			label = 'Login successful!';
			document.cookie = 'loggedIn=true; path=/; max-age=31536000';
			await goto('/account');
			document.cookie = `username=${encodeURIComponent(enteredUsername)}; path=/; max-age=31536000`;
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

{#if isLarge}
	<div class="min-h-screen flex items-center justify-center bg-black text-white text-2xl">
		<p>
			The <span class="text-[#6366FF] font-bold"> Metro Nexus </span> app cannot be opened on large screens.
		</p>
	</div>
{:else}
	<div
		class="min-h-screen w-full flex justify-center items-center p-5 bg-gradient-to-br from-[#000814] via-[#081225] to-[#1b2233] text-white"
	>
		<main
			class="w-[450px] min-h-[844px] p-8 rounded-[35px] bg-gradient-to-b from-[#020617] to-[#0f172a] flex flex-col justify-between"
		>
			<div>
				<div class="flex justify-between items-start">
					<div>
						<h1 class="text-[58px] font-bold leading-[0.9] tracking-tight">METRO<br />NEXUS</h1>
						<div class="mt-5">
							<p class="text-lg font-semibold">Your City.</p>
							<p class="text-lg font-semibold text-[#6366f1]">One Tap Ahead.</p>
						</div>
					</div>
					<div class="w-[115px] height-[115px] rounded-[20px] overflow-hidden">
						<img src="logo.png" alt="Logo" class="w-full h-full object-cover" />
					</div>
				</div>

				<div class="mt-20">
					{#if chosen === 'login'}
						<h2 class="text-[48px] font-bold">Welcome Back!</h2>
						<p class="text-[22px] text-gray-300">Sign in to continue your journey.</p>
					{:else}
						<h2 class="text-[48px] font-bold">Join Us!</h2>
						<p class="text-[22px] text-gray-300">Create an account to start your journey.</p>
					{/if}
				</div>

				<form
					onsubmit={(e) => {
						e.preventDefault();
						chosen === 'login' ? handleLogin() : handleRegister();
					}}
					class="mt-[50px]"
				>
					<div class="w-full h-[78px] bg-[#252c49] rounded-[20px] flex items-center px-5 mb-5">
						<div
							class="w-[55px] h-[55px] rounded-[15px] bg-[#6366f1] mr-5 flex-shrink-0 flex items-center justify-center"
						>
							<span class="material-symbols-outlined text-2xl text-white">alternate_email</span>
						</div>
						<div class="flex-1">
							<input
								type="text"
								placeholder="Username, Email or Phone Number"
								bind:value={enteredUsername}
								required
								class="w-full border-none outline-none bg-transparent text-white text-lg placeholder-slate-300"
							/>
						</div>
					</div>

					<div class="w-full h-[78px] bg-[#252c49] rounded-[20px] flex items-center px-5 mb-5">
						<div
							class="w-[55px] h-[55px] rounded-[15px] bg-[#6366f1] mr-5 flex-shrink-0 flex items-center justify-center"
						>
							<span class="material-symbols-outlined text-2xl text-white">password</span>
						</div>
						<div class="flex-1">
							<input
								type="password"
								placeholder="Password"
								bind:value={enteredPassword}
								required
								class="w-full border-none outline-none bg-transparent text-white text-lg placeholder-slate-300"
							/>
						</div>
					</div>

					{#if chosen === 'login'}
						<div class="text-right mt-[10px]">
							<a href="#forgot" class="text-[#6366f1] no-underline hover:underline text-sm"
								>Forgot Password?</a
							>
						</div>
					{/if}

					{#if label}
						<p class="mt-4 text-center text-sm font-medium tracking-wide text-indigo-300">
							{label}
						</p>
					{/if}

					<div class="mt-[60px]">
						<button
							type="submit"
							class="w-full h-[90px] border-none rounded-[25px] text-[38px] font-bold cursor-pointer bg-gradient-to-r from-[#6366f1] to-[#b8b8ff] text-white transition-opacity hover:opacity-90"
						>
							{chosen === 'login' ? 'Log In →' : 'Register →'}
						</button>
					</div>
				</form>
			</div>

			<div class="mt-12 text-center pb-4">
				{#if chosen === 'login'}
					<p class="text-gray-500 text-[20px]">Don't have an account?</p>
					<button
						type="button"
						onclick={() => {
							chosen = 'register';
							label = '';
						}}
						class="text-[#d0ffe9] text-[32px] font-bold mt-2 bg-transparent border-none cursor-pointer hover:underline"
					>
						Create Account →
					</button>
				{:else}
					<p class="text-gray-500 text-[20px]">Already have an account?</p>
					<button
						type="button"
						onclick={() => {
							chosen = 'login';
							label = '';
						}}
						class="text-[#d0ffe9] text-[32px] font-bold mt-2 bg-transparent border-none cursor-pointer hover:underline"
					>
						Sign In →
					</button>
				{/if}
			</div>
		</main>
	</div>
{/if}
