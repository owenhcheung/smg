<script context="module">
</script>

<script>
	import Player from '../lib/Player.svelte'

	let gearsetId = '1103c082-1c80-4bf3-bb56-83734971d5ea'
	export let itemId = []
	const gearsetURL = 'https://etro.gg/gearset/'
	const gearsetEndpoint = 'https://etro.gg/api/gearsets/'
	const itemEndpoint = 'https://etro.gg/api/equipment/'

	export let gearset = new Map()
	export let items = new Map()

	async function populateGearset() {
		// grabs gearset and maps json response to gearsetID
		const response = await fetch(gearsetEndpoint + gearsetId)
		const data = await response.json()

		gearset.set(gearsetId, data)

		// populates an array of all itemIds needed based on the json data (without duplicates)
		let set = [
			data.weapon,
			data.head,
			data.body,
			data.hands,
			data.legs,
			data.feet,
			data.offHand,
			data.ears,
			data.neck,
			data.wrists,
			data.fingerL,
			data.fingerR
		]

		set.forEach(item => {
			if (item != null && !itemId.includes(item)) {
				itemId.push(item)
			}
		})
		return gearset

		await Promise.all(
			itemId.map(async itemId => {
				const response = await fetch(itemEndpoint + itemId)
				const data = await response.json()

				items.set(itemId, data)
			})
		)
	}

	let promise1 = populateGearset()
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
					{#each gearsetId as i}
						<Player
							name={i}
							link={gearsetURL + i}
							weapon={items.get(gearsets.get(i).weapon).name}
							head={items.get(gearsets.get(i).head).name}
							body={items.get(gearsets.get(i).body).name}
							hands={items.get(gearsets.get(i).hands).name}
							legs={items.get(gearsets.get(i).legs).name}
							feet={items.get(gearsets.get(i).feet).name}
							offHand={items.get(gearsets.get(i).offHand).name}
							ears={items.get(gearsets.get(i).ears).name}
							neck={items.get(gearsets.get(i).neck).name}
							wrists={items.get(gearsets.get(i).wrists).name}
							fingerL={items.get(gearsets.get(i).fingerL).name}
							fingerR={items.get(gearsets.get(i).fingerR).name}
						/>
					{/each}
				{:catch error}
					<p style="color: red">{error.message}</p>
				{/await}
			</tbody>
		</table>
	</div>
</div>
