<script>
	import { onMount } from 'svelte';
	import { page } from '$app/stores';
	import { goto } from '$app/navigation';

	const STORAGE_KEY = 'bookedSeats';
	let bookedSeats = $state([]);

	let selectedCarriage = $state('start');

	// this lets thepage know ball knowledge about station
	let station = $derived($page.url.searchParams.get('station'));

	let trainStartEl = $state();
	let trainMidEl = $state();
	let trainEndEl = $state();

	function scrollToImg(el) {
		el?.scrollIntoView({ behavior: 'smooth', block: 'start' });
	}

	function selectCarriage(carriage, el) {
		selectedCarriage = carriage;
		scrollToImg(el);
	}

	onMount(() => {
		const saved = localStorage.getItem(STORAGE_KEY);
		if (saved) {
			bookedSeats = JSON.parse(saved);
		}
		if (!document.cookie.includes('loggedIn=true')) {
			async function redirect() {
				await goto('/');
			}
			redirect();
		}
	});

	function toggleSeat(seatNumber) {
		if (bookedSeats.includes(seatNumber)) {
			bookedSeats = bookedSeats.filter((s) => s !== seatNumber);
		} else {
			bookedSeats = [...bookedSeats, seatNumber];
		}
		localStorage.setItem(STORAGE_KEY, JSON.stringify(bookedSeats));
	}

	function theyveDoneItBoss() {
		if (bookedSeats.length === 0) {
			alert('Please select at least one seat before confirming.');
			return;
		}
		goto(
			'/confirmation?station=' +
				encodeURIComponent(station) +
				'&seats=' +
				bookedSeats.length.toString() +
				'&seatno=' +
				bookedSeats.toString()
		);
	}
</script>

<main class="bg-[#cfe7ff] flex h-screen">
	<a href="/account"
		><span class="material-symbols-outlined mt-1 ml-1" style="font-size: 3rem;">arrow_back</span></a
	>
	<aside class="w-64 p-4">
		{#if !station}
			<p class="text-4xl font-bold mt-10">Choose <br /> Seats</p>
		{:else}
			<p class="text-4xl font-bold mt-10">Booking for {station}</p>
		{/if}
		<br />
		<div class="flex flex-col gap-2">
			<button
				class="w-19 h-21 overflow-hidden"
				onclick={() => selectCarriage('start', trainStartEl)}
				><img
					src={selectedCarriage === 'start' ? '/trainstart_o1.png' : '/trainstart_o.png'}
					class="w-19"
					alt="yes"
				/></button
			>
			<button class="w-19 h-21 overflow-hidden" onclick={() => selectCarriage('mid', trainMidEl)}
				><img
					src={selectedCarriage === 'mid' ? '/trainmid_o1.png' : '/trainmid_o.png'}
					class="w-19"
					alt="yes2"
				/></button
			>
			<button class="w-19 h-21 overflow-hidden" onclick={() => selectCarriage('end', trainEndEl)}
				><img
					src={selectedCarriage === 'end' ? '/trainend_o1.png' : '/trainend_o.png'}
					class="w-19"
					alt="yes3"
				/></button
			>
		</div>
		<p class="mt-7 text-3xl">Seats</p>
		<p class="text-2xl mt-1 text-[#6366ff]">{bookedSeats.length}</p>
		<p class="mt-7 text-3xl">Amount</p>
		<p class="text-2xl mt-1 text-[#6366ff]">₹{bookedSeats.length * 60}</p>
		<img src="seats.png" class="mt-2" />
		<button
			class="bg-[#6366FF] text-white py-2 px-4 rounded-4xl mt-5 ml-3 mb-2"
			onclick={theyveDoneItBoss}>Book and Pay</button
		>
	</aside>
	<section class="flex-1 overflow-y-auto p-4 mt-10">
		<div class="relative w-32 ml-auto">
			<img
				bind:this={trainStartEl}
				src="/trainstart.png"
				alt="TrainStart"
				class="rounded-xl w-32 ml-auto"
			/>
			<button
				onclick={() => toggleSeat(1)}
				class="absolute top-19 left-1.5 h-9 w-9 rounded-lg {bookedSeats.includes(1)
					? 'bg-[#6366ff]'
					: 'bg-amber-200'}">01</button
			>
			<button
				onclick={() => toggleSeat(2)}
				class="absolute top-19 left-22 h-9 w-9 rounded-lg {bookedSeats.includes(2)
					? 'bg-[#6366ff]'
					: 'bg-amber-200'}">02</button
			>
			<button
				onclick={() => toggleSeat(3)}
				class="absolute top-30 left-1.5 h-9 w-9 rounded-lg {bookedSeats.includes(3)
					? 'bg-[#6366ff]'
					: 'bg-amber-200'}">03</button
			>
			<button class="absolute top-30 left-22 h-9 w-9 bg-[#bdf2de] rounded-lg">04</button>
			<button
				onclick={() => toggleSeat(5)}
				class="absolute top-48 left-1.5 h-9 w-9 rounded-lg {bookedSeats.includes(5)
					? 'bg-[#6366ff]'
					: 'bg-amber-200'}">05</button
			>
			<button
				onclick={() => toggleSeat(6)}
				class="absolute top-48 left-22 h-9 w-9 rounded-lg {bookedSeats.includes(6)
					? 'bg-[#6366ff]'
					: 'bg-amber-200'}">06</button
			>
			<button
				onclick={() => toggleSeat(7)}
				class="absolute top-59 left-1.5 h-9 w-9 rounded-lg {bookedSeats.includes(7)
					? 'bg-[#6366ff]'
					: 'bg-amber-200'}">07</button
			>
			<button
				onclick={() => toggleSeat(8)}
				class="absolute top-59 left-22 h-9 w-9 rounded-lg {bookedSeats.includes(8)
					? 'bg-[#6366ff]'
					: 'bg-amber-200'}">08</button
			>
			<button
				onclick={() => toggleSeat(9)}
				class="absolute top-70 left-1.5 h-9 w-9 rounded-lg {bookedSeats.includes(9)
					? 'bg-[#6366ff]'
					: 'bg-amber-200'}">09</button
			>
			<button class="absolute top-70 left-22 h-9 w-9 bg-[#bdf2de] rounded-lg">10</button>
			<button class="absolute top-88 left-1.5 h-9 w-9 bg-[#bdf2de] rounded-lg">11</button>
			<button class="absolute top-88 left-22 h-9 w-9 bg-[#bdf2de] rounded-lg">12</button>
			<button class="absolute top-99 left-1.5 h-9 w-9 bg-[#bdf2de] rounded-lg">13</button>
			<button
				onclick={() => toggleSeat(14)}
				class="absolute top-99 left-22 h-9 w-9 rounded-lg {bookedSeats.includes(14)
					? 'bg-[#6366ff]'
					: 'bg-amber-200'}">14</button
			>
		</div>
		<div class="relative w-32 ml-auto">
			<img
				bind:this={trainMidEl}
				src="/trainmid.png"
				alt="TrainMid"
				class="mt-5 rounded-xl w-32 ml-auto"
			/>
			<button
				onclick={() => toggleSeat(15)}
				class="absolute top-3 left-1.5 h-9 w-9 rounded-lg {bookedSeats.includes(15)
					? 'bg-[#6366ff]'
					: 'bg-amber-200'}">15</button
			>
			<button
				onclick={() => toggleSeat(16)}
				class="absolute top-3 left-22 h-9 w-9 rounded-lg {bookedSeats.includes(16)
					? 'bg-[#6366ff]'
					: 'bg-amber-200'}">16</button
			>
			<button class="absolute top-14 left-1.5 h-9 w-9 bg-[#bdf2de] rounded-lg">17</button>
			<button class="absolute top-14 left-22 h-9 w-9 bg-[#bdf2de] rounded-lg">18</button>
			<button class="absolute top-29.5 left-1.5 h-9 w-9 bg-[#bdf2de] rounded-lg">19</button>
			<button
				onclick={() => toggleSeat(20)}
				class="absolute top-29.5 left-22 h-9 w-9 rounded-lg {bookedSeats.includes(20)
					? 'bg-[#6366ff]'
					: 'bg-amber-200'}">20</button
			>
			<button
				onclick={() => toggleSeat(21)}
				class="absolute top-40.25 left-1.5 h-9 w-9 rounded-lg {bookedSeats.includes(21)
					? 'bg-[#6366ff]'
					: 'bg-amber-200'}">21</button
			>
			<button
				onclick={() => toggleSeat(22)}
				class="absolute top-40.25 left-22 h-9 w-9 rounded-lg {bookedSeats.includes(22)
					? 'bg-[#6366ff]'
					: 'bg-amber-200'}">22</button
			>
			<button
				onclick={() => toggleSeat(23)}
				class="absolute top-51.25 left-1.5 h-9 w-9 rounded-lg {bookedSeats.includes(23)
					? 'bg-[#6366ff]'
					: 'bg-amber-200'}">23</button
			>
			<button class="absolute top-51.25 left-22 h-9 w-9 bg-[#bdf2de] rounded-lg">24</button>
			<button
				onclick={() => toggleSeat(25)}
				class="absolute top-62.25 left-1.5 h-9 w-9 rounded-lg {bookedSeats.includes(25)
					? 'bg-[#6366ff]'
					: 'bg-amber-200'}">25</button
			>
			<button class="absolute top-62.25 left-22 h-9 w-9 bg-[#bdf2de] rounded-lg">26</button>
			<button
				onclick={() => toggleSeat(27)}
				class="absolute top-77.25 left-1.5 h-9 w-9 rounded-lg {bookedSeats.includes(27)
					? 'bg-[#6366ff]'
					: 'bg-amber-200'}">27</button
			>
			<button class="absolute top-77.25 left-22 h-9 w-9 bg-[#bdf2de] rounded-lg">28</button>
			<button
				onclick={() => toggleSeat(29)}
				class="absolute top-88.25 left-1.5 h-9 w-9 rounded-lg {bookedSeats.includes(29)
					? 'bg-[#6366ff]'
					: 'bg-amber-200'}">29</button
			>
			<button class="absolute top-88.25 left-22 h-9 w-9 bg-[#bdf2de] rounded-lg">30</button>
			<button
				onclick={() => toggleSeat(31)}
				class="absolute top-99.25 left-1.5 h-9 w-9 rounded-lg {bookedSeats.includes(31)
					? 'bg-[#6366ff]'
					: 'bg-amber-200'}">31</button
			>
			<button class="absolute top-99.25 left-22 h-9 w-9 bg-[#bdf2de] rounded-lg">32</button>
		</div>
		<div class="relative w-32 ml-auto">
			<img
				bind:this={trainEndEl}
				src="/trainstart.png"
				alt="TrainEnd"
				class="rotate-180 mt-5 rounded-xl w-32 ml-auto"
			/>
			<button
				onclick={() => toggleSeat(33)}
				class="absolute top-3.25 left-1.5 h-9 w-9 rounded-lg {bookedSeats.includes(33)
					? 'bg-[#6366ff]'
					: 'bg-amber-200'}">33</button
			>
			<button class="absolute top-3.25 left-22 h-9 w-9 bg-[#bdf2de] rounded-lg">34</button>
			<button class="absolute top-14.25 left-1.5 h-9 w-9 bg-[#bdf2de] rounded-lg">35</button>
			<button class="absolute top-14.25 left-22 h-9 w-9 bg-[#bdf2de] rounded-lg">36</button>
			<button class="absolute top-32.25 left-1.5 h-9 w-9 bg-[#bdf2de] rounded-lg">37</button>
			<button
				onclick={() => toggleSeat(38)}
				class="absolute top-32.25 left-22 h-9 w-9 rounded-lg {bookedSeats.includes(38)
					? 'bg-[#6366ff]'
					: 'bg-amber-200'}">38</button
			>
			<button
				onclick={() => toggleSeat(39)}
				class="absolute top-43.25 left-1.5 h-9 w-9 rounded-lg {bookedSeats.includes(39)
					? 'bg-[#6366ff]'
					: 'bg-amber-200'}">39</button
			>
			<button
				onclick={() => toggleSeat(40)}
				class="absolute top-43.25 left-22 h-9 w-9 rounded-lg {bookedSeats.includes(40)
					? 'bg-[#6366ff]'
					: 'bg-amber-200'}">40</button
			>
			<button
				onclick={() => toggleSeat(41)}
				class="absolute top-54.25 left-1.5 h-9 w-9 rounded-lg {bookedSeats.includes(41)
					? 'bg-[#6366ff]'
					: 'bg-amber-200'}">41</button
			>
			<button
				onclick={() => toggleSeat(42)}
				class="absolute top-54.25 left-22 h-9 w-9 rounded-lg {bookedSeats.includes(42)
					? 'bg-[#6366ff]'
					: 'bg-amber-200'}">42</button
			>
			<button class="absolute top-72.25 left-1.5 h-9 w-9 bg-[#bdf2de] rounded-lg">43</button>
			<button
				onclick={() => toggleSeat(44)}
				class="absolute top-72.25 left-22 h-9 w-9 rounded-lg {bookedSeats.includes(44)
					? 'bg-[#6366ff]'
					: 'bg-amber-200'}">44</button
			>
			<button
				onclick={() => toggleSeat(45)}
				class="absolute top-83.25 left-1.5 h-9 w-9 rounded-lg {bookedSeats.includes(45)
					? 'bg-[#6366ff]'
					: 'bg-amber-200'}">45</button
			>
			<button
				onclick={() => toggleSeat(46)}
				class="absolute top-83.25 left-22 h-9 w-9 rounded-lg {bookedSeats.includes(46)
					? 'bg-[#6366ff]'
					: 'bg-amber-200'}">46</button
			>
		</div>
	</section>
</main>
