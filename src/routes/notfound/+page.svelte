<script>
	import { goto } from '$app/navigation';
	import { onMount } from 'svelte';

	onMount(() => {
		if (!document.cookie.includes('loggedIn=true')) {
			async function redirect() {
				await goto('/');
			}
			redirect();
		}
	});
</script>

<main class="relative bg-[#111111] min-h-screen flex items-center justify-center">
	<a href="/account" class="absolute top-4 left-4">
		<span class="material-symbols-outlined text-white" style="font-size: 3rem;"> arrow_back </span>
	</a>

	<p class="text-2xl font-bold text-white">No tickets found.</p>
</main>
