<script>
	export let name = 'player name'
	export let weapon = 'weapon name'
	export let head = 'head name'
	export let body = 'body name'

	let gearsetLink = ''

	$: gearsetEndpoint =
		'https://etro.gg/api/gearsets/' +
		gearsetLink.replace(/\/\/*/g, '/').replace(/\/+$/, '').slice(23)
	$: equipmentEndpoint = 'https://etro.gg/api/equipment/'

	async function fetchGearset(gearset) {
		try {
			const response = await fetch(gearset)
			const data = await response.json()

			return [
				data.weapon,
				data.head,
				data.body,
				data.hands,
				data.legs,
				data.feet,
				data.ears,
				data.neck,
				data.wrists,
				data.fingerL,
				data.fingerR
			]
		} catch (error) {
			console.error('something fucked up', error.message, error.stack)
			return []
		}
	}

	async function fetchItemName(item) {
		const response = await fetch(item)
		const data = await response.json()

		return data.name
	}

	$: {
		if (gearsetLink) {
			let temp = []
			fetchGearset(gearsetEndpoint).then(gearset => {
				console.log(gearset)
				gearset.forEach(id =>
					fetchItemName(equipmentEndpoint + id).then(name => {
						temp.push(name)
					})
				)
			})
			console.log(temp)
			// console.log(fetchItemName(equipmentEndpoint + '40206'))
		}
	}
</script>

<tr>
	<td class="border px-8 py-4">
		<div class="flex items-baseline">
			<p class="mr-5">{name}</p>
			<input
				type="text"
				class="bg-stone-200 text-neutral-500 focus:text-black py-1 px-3 truncate focus:outline-none w-40"
				placeholder="input gearset link"
				bind:value={gearsetLink}
			/>
		</div>
	</td>
	<td class="border px-8 py-4">{weapon}</td>
	<td class="border px-8 py-4">{head}</td>
	<td class="border px-8 py-4">{body}</td>
</tr>

<style>
</style>
