<script context="module">
</script>

<script>
	import { onMount } from 'svelte'
	import Player from '../lib/Player.svelte'

	let gearsetId = ['1103c082-1c80-4bf3-bb56-83734971d5ea', 'f2426d1e-2da8-4151-bf52-74ca67b5f4a2']
	const gearsetURL = 'https://etro.gg/gearset/'
	const gearsetEndpoint = 'https://etro.gg/api/gearsets/'
	const equipmentEndpoint = 'https://etro.gg/api/equipment/'

	export let gearsets = new Map()
	//export let weapons = []

	async function populateGearsets() {
		await Promise.all(
			gearsetId.map(async gearsetId => {
				const response = await fetch(gearsetEndpoint + gearsetId)
				const data = await response.json()

				gearsets.set(gearsetId, data)
			})
		)
		return gearsets
	}

	let promise = populateGearsets()
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
				{#await promise}
					<p>...waiting</p>
				{:then gearsets}
					<Player
						name={'Warrior'}
						link={gearsetURL + gearsetId[0]}
						weapon={gearsets.get(gearsetId[0]).weapon}
						body={gearsets.get(gearsetId[0]).body}
					/>
					<Player
						name={'Bard'}
						link={gearsetURL + gearsetId[1]}
						weapon={gearsets.get(gearsetId[1]).weapon}
						body={gearsets.get(gearsetId[1]).body}
					/>
				{:catch error}
					<p style="color: red">{error.message}</p>
				{/await}
			</tbody>
		</table>
	</div>
</div>
