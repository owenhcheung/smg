<!-- <script context="module">
</script> -->

<script>
	import { onMount } from 'svelte'

	let id = '1103c082-1c80-4bf3-bb56-83734971d5ea'
	const endpoint = 'https://etro.gg/api/gearsets/' + id

	export let set1 = []

	onMount(async function () {
		const response = await fetch(endpoint)
		const data = await response.json()

		set1 = data
		console.log(set)
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
					<td class="border px-8 py-4">{set1.weapon}</td>
					<td class="border px-8 py-4">{set1.head}</td>
					<td class="border px-8 py-4">{set1.body}</td>
				</tr>
				<tr>
					<td class="border px-8 py-4">Player 2</td>
					<td class="border px-8 py-4">{set1.weapon}</td>
					<td class="border px-8 py-4">{set1.head}</td>
					<td class="border px-8 py-4">{set1.body}</td>
				</tr>
			</tbody>
		</table>
	</div>
</div>
