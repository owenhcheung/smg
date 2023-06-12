<script>
	export let name = 'player name'
	export let weapon = 'weapon name'
	export let head = 'head name'
	export let body = 'body name'

	export let link = 'input gearset'
</script>

<tr>
	<td class="border px-8 py-4">
		<div class="grid autogrid items-baseline">
			<p class="mr-5">{name}</p>
			<input
				type="text"
				class="bg-stone-200 text-neutral-500 focus:text-black py-1 px-3 truncate focus:outline-none w-32"
				bind:value={link}
			/>
		</div>
	</td>
	<td class="border px-8 py-4">{weapon}</td>
	<td class="border px-8 py-4">{head}</td>
	<td class="border px-8 py-4">{body}</td>
</tr>

<style>
	.autogrid {
		grid-template-columns: auto 1fr;
	}
</style>
