<script context="module">
</script>

<script>
	import Player from '../lib/Player.svelte'

	let gearsetId = '1103c082-1c80-4bf3-bb56-83734971d5ea'
	let equipmentId = []

	const gearsetURL = 'https://etro.gg/gearset/'
	const gearsetEndpoint = 'https://etro.gg/api/gearsets/'
	const equipmentEndpoint = 'https://etro.gg/api/equipment/'

	export let gearset = new Map()
	export let equipment = new Map()

	async function populateGearset() {
		// grabs gearset and maps json response to gearsetID
		const response = await fetch(gearsetEndpoint + gearsetId)
		const data = await response.json()

		gearset.set(gearsetId, data)

		return gearset
	}

	async function populateEquipment(gearset) {
		// populates an array of all itemIds needed based on the json data (without duplicates)
		let set = [
			gearset.get(gearsetId).weapon,
			gearset.get(gearsetId).head,
			gearset.get(gearsetId).body,
			gearset.get(gearsetId).hands,
			gearset.get(gearsetId).legs,
			gearset.get(gearsetId).feet,
			gearset.get(gearsetId).offHand,
			gearset.get(gearsetId).ears,
			gearset.get(gearsetId).neck,
			gearset.get(gearsetId).wrists,
			gearset.get(gearsetId).fingerL,
			gearset.get(gearsetId).fingerR
		]

		set.forEach(equipment => {
			if (equipment != null && !equipmentId.includes(equipment)) {
				equipmentId.push(equipment)
			}
		})

		await Promise.all(
			equipmentId.map(async equipmentId => {
				const response = await fetch(equipmentEndpoint + equipmentId)
				const data = await response.json()

				equipment.set(equipmentId, data)
			})
		)

		return equipment
	}

	let promise1 = populateGearset().then(gearset => populateEquipment(gearset))
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
				{#await promise1}
					<tr class="border">
						<td class="px-8 py-4">
							<p>Loading...</p>
						</td>
					</tr>
				{:then props}
					<Player
						name={gearsetId}
						link={gearsetURL + gearsetId}
						weapon={props.equipment.get(props.gearset.get(gearsetId).weapon).name}
					/>
				{:catch error}
					<p class="text-red">{error.message}</p>
				{/await}
			</tbody>
		</table>
	</div>
</div>
<!-- head={equipment.get(gearsets.get(i).head).name}
							body={equipment.get(gearsets.get(i).body).name}
							hands={equipment.get(gearsets.get(i).hands).name}
							legs={equipment.get(gearsets.get(i).legs).name}
							feet={equipment.get(gearsets.get(i).feet).name}
							offHand={equipment.get(gearsets.get(i).offHand).name}
							ears={equipment.get(gearsets.get(i).ears).name}
							neck={equipment.get(gearsets.get(i).neck).name}
							wrists={equipment.get(gearsets.get(i).wrists).name}
							fingerL={equipment.get(gearsets.get(i).fingerL).name}
							fingerR={equipment.get(gearsets.get(i).fingerR).name} -->
