<script context="module">
</script>

<script>
	import Player from '../lib/Player.svelte'
	let link = ''
</script>

<div class="flex w-screen h-screen p-20">
	<div class="w-full h-full">
		<!-- <p class="text-2xl font-bold mb-5">Loot Table</p> -->
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
				<Player name={'Warrior'} />
				<Player name={'Bard'} />
			</tbody>
		</table>
	</div>
</div>
