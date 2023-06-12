<!-- <script context="module">
</script> -->

<script>
	import { onMount } from 'svelte'
	import Player from '../lib/Player.svelte'

	let id = '1103c082-1c80-4bf3-bb56-83734971d5ea'
	const endpoint = 'https://etro.gg/api/gearsets/' + id

	export let set1 = []

	onMount(async function () {
		const response = await fetch(endpoint)
		const data = await response.json()

		set1 = data
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
				<Player
					name={'test'}
					weapon={set1.weapon}
					body={set1.body}
					link={'https://etro.gg/gearset/1103c082-1c80-4bf3-bb56-83734971d5ea'}
				/>
				<Player weapon={set1.weapon} head={set1.head} body={set1.body} />
				<Player name={'test'} weapon={set1.weapon} head={set1.head} body={set1.body} />
			</tbody>
		</table>
	</div>
</div>
