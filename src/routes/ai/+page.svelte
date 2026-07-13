<script lang="ts">
	import { GoogleGenAI } from '@google/genai';
	import { tick } from 'svelte';

	type Message = { role: 'user' | 'ai'; text: string };

	let whatDidZeUzerTypeBoss2 = $state('');
	let messages = $state<Message[]>([]);
	let loading = $state(false);
	let chatEl = $state<HTMLDivElement>();

	const ai = new GoogleGenAI({ apiKey: 'AIzaSyAczDzxln7eOL9NN1r18olRyQiSwEGDFrE' });

	async function abeGeminiChupChapBtaDe() {
		const query = whatDidZeUzerTypeBoss2.trim();
		if (!query || loading) return;

		messages.push({ role: 'user', text: query });
		whatDidZeUzerTypeBoss2 = '';
		loading = true;

		await tick();
		chatEl?.scrollTo({ top: chatEl.scrollHeight, behavior: 'smooth' });

		const response = await ai.models.generateContent({
			model: 'gemini-3.5-flash',
			contents:
				'You are a Metro Nexus AI assistant. Do not use Em Dashes and use Casual Language. Invent time details etc. when explicitly stated the user needs these details, when not asked for them, dont use anything. Keep your answers consicse and to-the-point, and the stations are: Aether, Aproxin University, Aurora, Bizin, Brenish Hospital, Bringon Valley, Celestia, Chiemy Stadium, Cilmic Lake, Cimpic Research Centre, Crocmon City, CYN, Dowgatry City Park, Eyalki Farms, Falcon Bay, Flux City, Gen Meta, Gravity Point, Helios, Horizon, Julia Street, Khidaio, Krimbu Jail, Lumora, Mukin Palace, Nemry Art Gallery, NP, Nunmree, Orion Gate, Pulkrin Street, Quantam Bay, Shiya Stand, Snorlax, Solaris, Sontech City, Specco Lane, Spiwell, Tihar Jail, Trumpet Community College, Unimick Zenith Mall, Versova Mart, Vertex, Vizania, VVK Hospital, Xitazo Institute of Technology, Yashmin, Youtrete, Zenith, Ziggi Zoo. Answer the users query helpfully, and without using any markdown or html formatting. Their query is: ' +
				query
		});

		messages.push({ role: 'ai', text: response.text ?? '(no response)' });
		loading = false;

		await tick();
		chatEl?.scrollTo({ top: chatEl.scrollHeight, behavior: 'smooth' });
	}

	function handleKeydown(e: KeyboardEvent) {
		if (e.key === 'Enter') abeGeminiChupChapBtaDe();
	}
</script>

<main class="bg-[#111111] min-h-screen flex flex-col">
	{#if messages.length === 0}
		<div class="flex-1 flex flex-col gap-4 px-4 mt-10">
			<img src="ai.png" alt="Nexus AI Logo" class="w-full h-48 object-cover object-center" />
			<p class="text-white text-4xl text-center font-bold">
				Nexus <span class="text-[#6366FF]">AI</span>
			</p>
			<p class="text-gray-400 text-center">
				Your smart travel assistant, <br /> Ask anything. Get instant Answers
			</p>
			<div class="mt-20">
				<p class="font-bold text-white">Suggestions:</p>
				<button
					onclick={() => {
						whatDidZeUzerTypeBoss2 =
							'What are some Services at Aurora Staion? (Food, Water, a Hotel etc.)';
						abeGeminiChupChapBtaDe();
					}}
					class="h-20 text-gray-300 flex items-center w-full"
					><span class="material-symbols-outlined text-white mr-2">accessibility</span>Services at
					Aurora
					<span class="ml-auto material-symbols-outlined text-white"> arrow_forward </span>
				</button>
				<hr class="border border-white" />
				<button
					onclick={() => {
						whatDidZeUzerTypeBoss2 = 'What is the next train to Orion Gate?';
						abeGeminiChupChapBtaDe();
					}}
					class="h-20 text-gray-300 flex items-center w-full"
					><span class="material-symbols-outlined text-white mr-2">event</span> Next Route to Orion
					Gate <span class="ml-auto material-symbols-outlined text-white"> arrow_forward </span>
				</button>
				<hr class="border border-white" />
				<button
					onclick={() => {
						whatDidZeUzerTypeBoss2 =
							'Where is the Lost and Found? (the answer is at the station help desk, invent some details but not many)';
						abeGeminiChupChapBtaDe();
					}}
					class="h-20 text-gray-300 flex items-center w-full"
					><span class="material-symbols-outlined text-white mr-2">search_check</span>Lost and Found
					<span class="ml-auto material-symbols-outlined text-white"> arrow_forward </span>
				</button>
			</div>
			<div class="w-full max-w-md h-20 rounded-4xl border-2 px-1 flex items-center text-white">
				<input
					class="flex-1 bg-transparent rounded-4xl border-none focus:outline-none focus:ring-0"
					placeholder="Ask Nexus AI anything..."
					bind:value={whatDidZeUzerTypeBoss2}
					onkeydown={handleKeydown}
				/>
				<button
					onclick={abeGeminiChupChapBtaDe}
					class="rounded-4xl bg-[#6366FF] h-13 w-9 material-symbols-outlined shrink-0"
					><span class="text-white material-symbols-outlined">arrow_forward</span></button
				>
			</div>
			<div>
				<div
					class="mx-auto w-82 rounded-[10rem] h-20 border-2 border-white flex items-center justify-center"
				>
					<button>
						<a href="/rewards">
							<img src="icons/star.png" class="h-7 ml-4 mr-4" alt="chand tara" />
						</a>
					</button>
					<button>
						<a href="/ai">
							<img src="icons/robot_s.png" class="h-12 ml-4 mr-4" alt="chateshgpt" />
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
		</div>
	{:else}
		<div class="p-4">
			<p class="text-white text-2xl font-bold">Nexus AI</p>
		</div>

		<div bind:this={chatEl} class="flex-1 overflow-y-auto px-4 flex flex-col gap-3">
			{#each messages as message}
				<div class="flex {message.role === 'user' ? 'justify-end' : 'justify-start'}">
					<p
						class="max-w-[75%] px-4 py-2 rounded-3xl text-white {message.role === 'user'
							? 'bg-[#6366FF]'
							: 'bg-[#222222]'}"
					>
						{message.text}
					</p>
				</div>
			{/each}

			{#if loading}
				<div class="flex justify-start">
					<p class="max-w-[75%] px-4 py-2 rounded-3xl text-white bg-[#222222] animate-pulse">
						Thinking...
					</p>
				</div>
			{/if}
		</div>

		<div class="p-4">
			<div
				class="w-full max-w-md mx-auto h-12 rounded-4xl border-2 px-1 flex items-center text-white"
			>
				<input
					class="flex-1 bg-transparent rounded-4xl border-none focus:outline-none focus:ring-0"
					placeholder="Ask Nexus AI anything..."
					bind:value={whatDidZeUzerTypeBoss2}
					onkeydown={handleKeydown}
					disabled={loading}
				/>
				<button
					onclick={abeGeminiChupChapBtaDe}
					disabled={loading}
					class="rounded-4xl bg-[#6366FF] h-9 w-11 material-symbols-outlined shrink-0 disabled:opacity-50"
					><span class="text-white material-symbols-outlined">arrow_forward</span></button
				>
			</div>
		</div>
	{/if}
</main>
