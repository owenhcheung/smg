<!-- <script context="module">
</script> -->

<script>
	import { onMount } from 'svelte'

	let id = '1103c082-1c80-4bf3-bb56-83734971d5ea'
	const endpoint = 'https://etro.gg/api/gearsets/' + id

	export let set = []

	onMount(async function () {
		const response = await fetch(endpoint)
		const data = await response.json()

		set = data
	})
</script>

<div class="flex w-screen h-screen p-20">
	<div class="w-full h-full">
		<h1 class="mb-5">gearset</h1>
		<ul>
			<li>
				weapon: {set.weapon}
			</li>
		</ul>
	</div>
</div>
