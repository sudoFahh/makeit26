<script lang="ts">
	import { Modal, Content, Trigger } from 'sv-popup';
	import { onMount } from 'svelte';
	import { goto } from '$app/navigation';

	// replace with name from signup form later
	let name = $state('User');
	let whatDidZeUzerTypeBoss = $state('');
	const stations = [
		'Aether',
		'Aproxin University',
		'Aurora',
		'Bizin',
		'Brenish Hospital',
		'Bringon Valley',
		'Celestia',
		'Chiemy Stadium',
		'Cilmic Lake',
		'Cimpic Research Centre',
		'Crocmon City',
		'CYN',
		'Dowgatry City Park',
		'Eyalki Farms',
		'Falcon Bay',
		'Flux City',
		'Gen Meta',
		'Gravity Point',
		'Helios',
		'Horizon',
		'Julia Street',
		'Khidaio',
		'Krimbu Jail',
		'Lumora',
		'Mukin Palace',
		'Nemry Art Gallery',
		'NP',
		'Nunmree',
		'Orion Gate',
		'Pulkrin Street',
		'Quantam Bay',
		'Shiya Stand',
		'Snorlax',
		'Solaris',
		'Sontech City',
		'Specco Lane',
		'Spiwell',
		'Tihar Jail',
		'Trumpet Community College',
		'Unimick Zenith Mall',
		'Versova Mart',
		'Vertex',
		'Vizania',
		'VVK Hospital',
		'Xitazo Institute of Technology',
		'Yashmin',
		'Youtrete',
		'Zenith',
		'Ziggi Zoo'
	];

	onMount(() => {
		if (!document.cookie.includes('loggedIn=true')) {
			async function redirect() {
				await goto('/');
			}
			redirect();
		}
	});

	function checkForStations() {
		if (whatDidZeUzerTypeBoss.length > 0) {
			const foundStation = stations.find(
				(station) => station.toLowerCase() === whatDidZeUzerTypeBoss.toLowerCase()
			);
			if (foundStation) {
				goto('/booking?station=' + encodeURIComponent(foundStation));
			} else {
				alert('Station not found. Please try again.');
			}
		}
	}
</script>

<main class="p-12 bg-[#111111] text-white min-h-screen">
	<p class="text-3xl font-bold">
		Namaste, <br /> <span class="text-[#6366FF] text-5xl">{name}</span>
	</p>
	<p class="text-xl">Where would you like to go today?</p>
	<div class="mt-5 flex items-center w-full h-12 rounded-4xl border-2 px-1">
		<input
			class="flex bg-transparent rounded-4xl w-full border-none focus:outline-none focus:ring-0"
			placeholder="Aurora"
			bind:value={whatDidZeUzerTypeBoss}
		/>
		<button
			onclick={checkForStations}
			class="rounded-4xl bg-[#6366FF] h-9 w-11 material-symbols-outlined"
			><span class="text-white material-symbols-outlined">arrow_forward</span></button
		>
	</div>
	<Modal>
		<Content>
			<h2>
				<img src="/map.png" alt="Map" class="rounded-xl" />
			</h2>
		</Content>
		<Trigger>
			<button>
				<img src="/startlocation.png" alt="Where you are right now" class="mt-10 rounded-xl" />
			</button>
		</Trigger>
	</Modal>
	<div>
		<div class="rounded-xl w-full mt-5 bg-[#222222]">
			<div class="text-center p-3">
				<p class="text-xl flex items-center justify-between">
					<span>Aurora</span>
					<span class="material-symbols-outlined">arrow_forward</span>
					<span>Orion Gate</span>
				</p>
				<p class="flex items-center justify-between mt-1">
					<span>09:00 AM</span>
					<span>09:45 AM</span>
				</p>
			</div>
			<p class="text-s text-gray-400 ml-3">19 Sept • 1 Passenger • Economy</p>
			<button class="bg-[#6366FF] text-white py-2 px-4 rounded-4xl mt-2 ml-3 mb-2"
				><a href="/booking" class="text-white">Buy Ticket Now</a></button
			>
			<span class="ml-69 text-xs rounded-lg bg-[#6366FF] text-white p-1">20% Discount!</span>
		</div>
		<div class="rounded-xl w-full mt-5 bg-[#222222]">
			<div class="text-center p-3">
				<p class="text-xl flex items-center justify-between">
					<span>Aurora</span>
					<span class="material-symbols-outlined">arrow_forward</span>
					<span>Volcania</span>
				</p>
				<p class="flex items-center justify-between mt-1">
					<span>09:00 AM</span>
					<span>09:20 AM</span>
				</p>
			</div>
			<p class="text-s text-gray-400 ml-3">20 Sept • 1 Passenger • Economy</p>
			<button class="bg-[#6366FF] text-white py-2 px-4 rounded-4xl mt-2 ml-3 mb-2"
				><a href="/booking" class="text-white">Buy Ticket Now</a></button
			>
			<span class="ml-69 text-xs rounded-lg bg-[#6366FF] text-white p-1">25% Discount!</span>
		</div>
	</div>
</main>
