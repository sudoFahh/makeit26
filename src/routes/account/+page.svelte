<script lang="ts">
	import { onMount } from 'svelte';
	import { goto } from '$app/navigation';

	onMount(() => {
		if (!document.cookie.includes('loggedIn=true')) {
			async function redirect() {
				await goto('/');
			}
			redirect();
		}
	});
</script>

<main class="p-12 bg-black text-white min-h-screen">
	<p class="text-3xl font-bold">Namaste Passenger!</p>
	<p class="text-xl">Where would you like to go today?</p>
	<div class="mt-5 flex items-center w-full h-12 rounded-4xl border-2 px-1">
		<input
			class="flex bg-transparent rounded-4xl w-full border-none focus:outline-none focus:ring-0"
			placeholder="Aurora"
		/>
		<button class="rounded-4xl bg-[#6366FF] h-9 w-11 material-symbols-outlined"
			>arrow_forward</button
		>
	</div>
	<img src="/startlocation.png" alt="Where you are right now" class="mt-10 rounded-xl" />
</main>
