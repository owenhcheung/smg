<script>
	export let name = 'player name'
	export let weapon = 'weapon name'
	export let head = 'head name'
	export let body = 'body name'

	export let link = 'https://etro.gg/gearset/1103c082-1c80-4bf3-bb56-83734971d5ea'
</script>

<tr>
	<td class="border px-8 py-4">
		{name}
		<input
			type="text"
			class="bg-stone-200 py-1 px-3 ml-5 truncate focus:outline-none"
			bind:value={link}
		/>
	</td>
	<td class="border px-8 py-4">{weapon}</td>
	<td class="border px-8 py-4">{head}</td>
	<td class="border px-8 py-4">{body}</td>
</tr>
