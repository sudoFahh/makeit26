<script>
	import { page } from '$app/stores';
	let station = $derived($page.url.searchParams.get('station'));
	let seats = $derived(Number($page.url.searchParams.get('seats')));
	let seatno = $derived($page.url.searchParams.get('seatno'));
	let coach = $state('');

	if (seatno[0] < 14) {
		coach = '1A';
	} else if (seatno[0] > 14 && seatno[0] < 31) {
		coach = '2B';
	} else {
		coach = '3C';
	}

	let name = $state('Manik');
</script>

<main class="bg-[#111111] min-h-screen px-4 py-6 sm:px-8">
	<div class="w-full bg-[#222222] flex flex-row items-center rounded-3xl p-4 gap-3">
		<div class="text-3xl shrink-0">✅</div>
		<section class="flex-1 min-w-0">
			<p class="text-white text-xl font-bold">You're all set!</p>
			<p class="text-white text-sm">
				Your ticket to {station} for {seats < 2 ? `${seats} seat` : `${seats} seats`} has been confirmed.
			</p>
		</section>
	</div>

	<img
		src="/startlocation.png"
		alt="Where you are right now"
		class="mt-8 rounded-xl w-full h-auto"
	/>

	<div class="relative rounded-xl w-full mt-5 bg-[#222222] overflow-hidden">
		<img src="ticketui.png" alt="Ticket" class="w-full h-auto" />

		<span class="absolute top-3 right-3 rounded-xl bg-[#6c6ed1] p-1 font-normal text-sm text-white">
			Standard
		</span>

		<div
			class="absolute top-3 left-3 right-20 gap-10 flex items-center text-white text-xl font-bold flex-nowrap overflow-hidden"
		>
			<span class="shrink-0">Aurora</span>
			<span class="material-symbols-outlined shrink-0">arrow_forward</span>
			<span class="truncate">{station}</span>
		</div>

		<div class="absolute top-11 left-3 right-3 flex items-center gap-11 text-white text-sm">
			<p>Today • No route Changes</p>
		</div>

		<div class="absolute top-22 left-3 right-3 flex items-center text-white text-sm">
			<p class="font-bold text-3xl">11:00</p>
			<img src="train.png" class="w-50" alt="simple icon" />
			<p class="font-bold text-3xl">13:45</p>
		</div>

		<div
			class="absolute top-40 left-8 right-3 flex items-center text-center gap-7 text-white text-sm"
		>
			<p class="font-extralight text-2xl">
				Passenger <br /> <span class="text-xl font-bold">{name}</span>
			</p>
			<p class="font-extralight text-2xl">
				Coach <br /> <span class="text-xl font-bold">{coach}</span>
			</p>
			<p class="font-extralight text-2xl">
				Seat <br /> <span class="text-xl font-bold">{seatno}</span>
			</p>
		</div>
		<div
			class="absolute top-80 left-8 right-3 flex items-center text-center gap-7 text-white text-sm"
		>
			<img src="qr-code.png" alt="QR Code" class="h-30 rounded-xl" />
		</div>
		<div
			class="absolute top-82 left-50 right-3 flex items-center text-center gap-7 text-white text-sm"
		>
			<p class="text-xl">
				Booking Refrence <br /> <span class="font-bold text-3xl">VYA-7K2Q</span> <br />
				<span class="text-sm">Show this code at the gate</span>
			</p>
		</div>
	</div>
</main>
