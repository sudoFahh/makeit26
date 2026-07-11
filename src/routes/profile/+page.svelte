<script lang="ts">
	let name = $state('Manik');
	let initial = $state(name[0]);
	let email = $state('a@example.com');

	function theyveDoneItBoss3() {
		alert('add kal');
	}
</script>

<main class="text-white bg-[#111111] min-h-screen min-w-screen">
	<br />
	<p class="text-2xl font-bold ml-2">My Profile</p>
	<p class="ml-2 mb-5">Manage your account and prefrences</p>
	<div class="w-[95%] ml-2.5 bg-[#363636] flex flex-row items-center rounded-3xl p-4 gap-3">
		<img class="text-3xl shrink-0" src="userimg.png" alt="userpng" />
		<div class="absolute top-44 left-21 right-5 flex items-center gap-11 text-white text-5xl">
			<p>{initial}</p>
		</div>
		<section class="flex-1 min-w-0">
			<p class="text-white text-4xl font-bold">{name}</p>
			<p>{email}</p>
		</section>
	</div>
	<div class="mt-20 ml-2.5 p-1 bg-[#363636] rounded-xl w-[95%]">
		<p class="font-bold text-2xl">Personal Information:</p>
		<hr class="border border-white w-90 mt-1 mb-1" />
		<p class="text-xl"><span class="material-symbols-outlined"> person </span> Name: {name}</p>
		<hr class="border border-white w-90 mt-1 mb-1" />
		<p class="text-xl">
			<span class="material-symbols-outlined"> alternate_email </span> Email Address: {email}
		</p>
		<hr class="border border-white w-90 mt-1 mb-1" />
		<p class="text-xl">
			<span class="material-symbols-outlined"> date_range </span>Date of Birth: 28 May 2012
		</p>
		<hr class="border border-white w-90 mt-1 mb-1" />
		<p class="text-xl">
			<span class="material-symbols-outlined"> location_city </span> Primary City: Aurora
		</p>
		<hr class="border border-white w-90 mt-1 mb-1" />
	</div>
	<button
		class="bg-[#6366FF] text-white py-2 px-4 rounded-4xl mt-5 ml-3 mb-2 w-[95%]"
		onclick={theyveDoneItBoss3}>Logout</button
	>
</main>
