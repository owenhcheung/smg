<script>
	export let name = 'player name'
	export let weapon = 'weapon name'
	export let head = 'head name'
	export let body = 'body name'
	export let hands = 'body name'
	export let legs = 'legs name'
	export let feet = 'feet name'
	export let offHand = 'offHand name'
	export let ears = 'ears name'
	export let neck = 'neck name'
	export let wrists = 'wrists name'
	export let fingerL = 'fingerL name'
	export let fingerR = 'fingerR name'

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
	<td class="border px-8 py-4">{hands}</td>
	<td class="border px-8 py-4">{legs}</td>
	<td class="border px-8 py-4">{feet}</td>
	<td class="border px-8 py-4">{offHand}</td>
	<td class="border px-8 py-4">{ears}</td>
	<td class="border px-8 py-4">{neck}</td>
	<td class="border px-8 py-4">{wrists}</td>
	<td class="border px-8 py-4">{fingerL}</td>
	<td class="border px-8 py-4">{fingerR}</td>
</tr>
