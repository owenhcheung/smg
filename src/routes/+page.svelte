<script context="module">
</script>

<script>
	import { onMount } from 'svelte'

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
		<table class="table-auto w-full shadow-lg text-sm">
			<thead>
				<tr>
					<th class="bg-slate-100 border text-left px-8 py-4">Name</th>
					<th class="bg-slate-100 border text-left px-8 py-4">Weapon</th>
					<th class="bg-slate-100 border text-left px-8 py-4">Head</th>
					<th class="bg-slate-100 border text-left px-8 py-4">Body</th>
				</tr>
			</thead>
			<tbody>
				<tr>
					<td class="border px-8 py-4">Player 1</td>
					<td class="border px-8 py-4">{gearsets[0]}</td>
					<td class="border px-8 py-4">{gearsets}</td>
					<td class="border px-8 py-4">{gearsets}</td>
				</tr>
			</tbody>
		</table>
	</div>
</div>
