<script context="module">
</script>

<script>
	import { onMount } from 'svelte'
	import Player from '../lib/Player.svelte'

	let gearsetId = ['1103c082-1c80-4bf3-bb56-83734971d5ea', 'f2426d1e-2da8-4151-bf52-74ca67b5f4a2']
	const gearsetEndpoint = 'https://etro.gg/api/gearsets/'
	const equipmentEndpoint = 'https://etro.gg/api/equipment/'

	export let gearsets = new Map()
	//export let weapons = []

	onMount(async () => {
		//const files = await getFilePaths();

		await Promise.all(
			gearsetId.map(async gearsetId => {
				const response = await fetch(gearsetEndpoint + gearsetId)
				const data = await response.json()

				gearsets.set(gearsetId, data)
			})
		).then(console.log(gearsets))
	})
</script>

<div class="flex w-screen h-screen p-20">
	<div class="w-full h-full">
		<p class="text-2xl font-bold mb-5">Loot Table</p>
		<table class="table-auto w-full shadow-lg">
			<thead>
				<tr>
					<th class="bg-stone-100 border text-left px-8 py-4">Name</th>
					<th class="bg-stone-100 border text-left px-8 py-4">Weapon</th>
					<th class="bg-stone-100 border text-left px-8 py-4">Head</th>
					<th class="bg-stone-100 border text-left px-8 py-4">Body</th>
				</tr>
			</thead>
			<tbody>
				<tr>
					<td class="border px-8 py-4">Player 1</td>
					<Player name={'test'} weapon={set1.weapon} body={set1.body} />
					<Player weapon={set1.weapon} head={set1.head} body={set1.body} />
					<Player name={'test'} weapon={set1.weapon} head={set1.head} body={set1.body} />
				</tr>
			</tbody>
		</table>
	</div>
</div>
