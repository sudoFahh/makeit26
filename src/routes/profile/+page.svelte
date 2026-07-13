<script lang="ts">
	import { goto } from '$app/navigation';
	import { onMount } from 'svelte';

	let name = $state('Pranav');
	let initial = $state(name[0]);
	let email = $state(name + '@example.com');

	onMount(() => {
		name = decodeURIComponent(
			document.cookie
				.split('; ')
				.find((c) => c.startsWith('username='))
				?.split('=')[1] ?? name
		);
		initial = name.charAt(0);
		email = name + '@example.com';
	});

	onMount(() => {
		if (!document.cookie.includes('loggedIn=true')) {
			async function redirect() {
				await goto('/');
			}
			redirect();
		}
	});

	function theyveDoneItBoss3() {
		document.cookie.split(';').forEach((cookie) => {
			const eqPos = cookie.indexOf('=');
			const name = (eqPos > -1 ? cookie.slice(0, eqPos) : cookie).trim();
			document.cookie = `${name}=; expires=Thu, 01 Jan 1970 00:00:00 GMT; path=/`;
		});
		goto('/');
	}
</script>

<main class="text-white bg-[#111111] min-h-screen w-full pb-10">
	<br />
	<div
		class="w-[95%] mx-auto bg-[#363636] flex flex-col md:flex-row items-center rounded-3xl p-6 gap-6"
	>
		<div class="flex flex-1 items-center gap-4 w-full">
			<div
				class="relative shrink-0 w-24 h-24 flex items-center justify-center bg-indigo-600 rounded-full text-5xl font-bold text-white"
			>
				{initial}
			</div>
			<div class="min-w-0">
				<p class="text-white text-3xl font-bold truncate">{name}</p>
				<p class="text-gray-300 truncate">{email}</p>
			</div>
		</div>

		<div class="bg-[#1c1c1e] w-full max-w-[400px] rounded-[20px] p-5 shadow-xl shrink-0">
			<div class="flex justify-between items-center text-white mb-4">
				<h2 class="text-xl font-semibold">Wallet</h2>
				<a href="#" class="text-[#7c86ff] text-sm">View Transactions</a>
			</div>

			<div class="flex gap-[10px] mb-4">
				<div
					class="flex-1 bg-gradient-to-br from-[#6a5ff5] to-[#4338ca] rounded-2xl p-4 text-white"
				>
					<p class="text-xs opacity-80 mb-1">Current Balance</p>
					<h1 class="text-2xl font-bold">₹1780</h1>
					<button
						class="bg-white/20 text-white border-none py-1.5 px-3 rounded-full mt-[14px] text-xs font-medium tracking-wide transition-all cursor-pointer"
					>
						+ Add Money
					</button>
				</div>

				<div class="flex-1 bg-[#141414] rounded-2xl p-4 text-white flex flex-col justify-between">
					<div>
						<p class="text-xs opacity-50 mb-1">Wallet ID</p>
						<h3 class="text-sm font-semibold tracking-wider">MTX ** 3456</h3>
					</div>
					<p class="text-[11px] text-red-400 mt-2 leading-tight">
						Low Balance alert<br /><span class="opacity-60">&lt;100</span>
					</p>
				</div>
			</div>

			<div
				class="bg-[#141414] rounded-2xl p-4 flex justify-around text-white text-center text-[11px]"
			>
				<div class="cursor-pointer group">
					<div
						class="w-[32px] h-[32px] rounded-full bg-[#4b3fc9] flex items-center justify-center mx-auto mb-1 transition-colors"
					>
						<img src="icons/plus.png" alt="+" />
					</div>
					Add Money
				</div>

				<div class="cursor-pointer group">
					<div
						class="w-[32px] h-[32px] rounded-full bg-[#4b3fc9] flex items-center justify-center mx-auto mb-1 transition-colors"
					>
						<img src="icons/s.png" alt="send" />
					</div>
					Send
				</div>

				<div class="cursor-pointer group">
					<div
						class="w-[32px] h-[32px] rounded-full bg-[#4b3fc9] flex items-center justify-center mx-auto mb-1 transition-colors"
					>
						<img src="icons/time.png" alt="time" />
					</div>
					History
				</div>

				<div class="cursor-pointer group">
					<div
						class="w-[32px] h-[32px] rounded-full bg-[#4b3fc9] flex items-center justify-center mx-auto mb-1 transition-colors"
					>
						<img src="icons/q.png" alt="ques" />
					</div>
					Help
				</div>
			</div>
		</div>
	</div>

	<div class="mt-2 mx-auto p-4 bg-[#363636] rounded-xl w-[95%] space-y-3">
		<p class="font-bold text-xl">Personal Information:</p>
		<hr class="border-gray-600 w-full" />
		<p class="flex items-center gap-2">
			<span class="material-symbols-outlined"> person </span> Name: {name}
		</p>
		<hr class="border-gray-600 w-full" />
		<p class="flex items-center gap-2">
			<span class="material-symbols-outlined"> alternate_email </span> Email Address: {email}
		</p>
		<hr class="border-gray-600 w-full" />
		<p class="flex items-center gap-2">
			<span class="material-symbols-outlined"> date_range </span>Date of Birth: 28 May 2012
		</p>
		<hr class="border-gray-600 w-full" />
		<p class="flex items-center gap-2">
			<span class="material-symbols-outlined"> location_city </span> Primary City: Aurora
		</p>
		<button
			class="bg-[#6366FF] py-3 px-4 rounded-full mt-5 block mx-auto w-[95%] font-medium transition-colors h-10"
			onclick={theyveDoneItBoss3}
		>
			Logout
		</button>
	</div>

	<div>
		<div
			class="mx-auto w-82 rounded-[10rem] h-20 border-2 border-white flex items-center justify-center mt-3"
		>
			<button>
				<a href="/rewards">
					<img src="icons/star.png" class="h-7 ml-4 mr-4" alt="chand tara" />
				</a>
			</button>
			<button>
				<a href="/ai">
					<img src="icons/robot.png" class="h-9 ml-4 mr-4" alt="chateshgpt" />
				</a>
			</button>
			<button>
				<a href="/account">
					<img src="icons/ghar.png" class="h-7 ml-4 mr-4" alt="ghar" />
				</a>
			</button>
			<button>
				<a href="/notfound">
					<img src="icons/ticket.png" class="h-7 ml-4 mr-4" alt="condicter sahib" />
				</a>
			</button>
			<button>
				<a href="/profile">
					<img src="icons/person_s.png" class="h-12 ml-4 mr-4" alt="banda" />
				</a>
			</button>
		</div>
	</div>
</main>
