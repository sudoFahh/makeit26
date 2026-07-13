<script lang="ts">
	import { Modal, Content, Trigger } from 'sv-popup';
</script>

<main class="bg-[#111111] text-white min-h-screen p-6">
	<h1 class="text-5xl font-bold">Rewards</h1>
	<p class="font-bold">Ride more, Earn more</p>
	<img src="rewards_nopadd.png" alt="bigrewardsfsfs" class="w-100 mt-[9.5%]" />
	<div>
		<p class="text-xl font-bold mt-[4.5%]">Membership Plans</p>
		<p>Get more rides for less</p>
		<div class="mt-[4.5%]">
			<div class="rounded-4xl bg-[#222222] p-4">
				<div class="flex items-center justify-between">
					<p class="font-bold">Metro Lite</p>
					<span class="font-normal">₹199 / Month</span>
				</div>
				<div class="rounded-2xl bg-[#363636]">
					<div class="p-2 flex items-center gap-3">
						<div class="text-sm">
							<span class="text-[#6366FF] font-bold text-base">20</span>
							<span class="text-[#6366FF] text-sm"> free rides</span><br />
							per month
						</div>
						<div class="h-10 w-1 bg-white"></div>
						<p class="text-sm">Extra rides <br /> ₹10 per ride</p>
						<div class="h-10 w-1 bg-white"></div>
						<p class="text-sm">Valid for <br /> 30 days</p>
						<Modal>
							<Content>
								<div class="bg-[#111111] p-6 rounded-2xl shadow-xl text-center min-w-[250px]">
									<p class="text-white font-semibold">Plan selected, Thank You!</p>
								</div>
							</Content>
							<Trigger>
								<button
									style="background: linear-gradient(157deg, #667eea 0%, #2f3176 100%);"
									class="p-2 rounded-2xl"
								>
									Select
								</button>
							</Trigger>
						</Modal>
					</div>
				</div>
			</div>
			<div class="rounded-4xl bg-[#222222] p-4 mt-10">
				<div class="flex items-center justify-between">
					<p class="font-bold">Metro Plus</p>
					<span class="font-normal">₹349 / Month</span>
				</div>
				<div class="rounded-2xl bg-[#363636]">
					<div class="p-2 flex items-center gap-3">
						<div class="text-sm">
							<span class="text-[#6366FF] font-bold text-base">40</span>
							<span class="text-[#6366FF] text-sm"> free rides</span><br />
							per month
						</div>
						<div class="h-10 w-1 bg-white"></div>
						<p class="text-sm">Extra rides <br /> ₹8 per ride</p>
						<div class="h-10 w-1 bg-white"></div>
						<p class="text-sm">Valid for <br /> 30 days</p>
						<Modal>
							<Content>
								<div class="bg-[#111111] p-6 rounded-2xl shadow-xl text-center min-w-[250px]">
									<p class="text-white font-semibold">Plan selected, Thank You!</p>
								</div>
							</Content>
							<Trigger>
								<button
									style="background: linear-gradient(157deg, #667eea 0%, #2f3176 100%);"
									class="p-2 rounded-2xl"
								>
									Select
								</button>
							</Trigger>
						</Modal>
					</div>
				</div>
			</div>
		</div>
	</div>
	<div>
		<div
			class="rounded-[10rem] h-20 border-2 mt-[25%] border-neutral-50 flex items-center justify-center"
		>
			<button>
				<a href="/rewards">
					<img src="icons/star_s.png" class="h-12 ml-4 mr-4" alt="chand tara" />
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
					<img src="icons/person.png" class="h-7 ml-4 mr-4" alt="banda" />
				</a>
			</button>
		</div>
	</div>
</main>
