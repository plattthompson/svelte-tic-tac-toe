<script>
	import { createEventDispatcher } from 'svelte';
	export let squareValue;
	export let rowValue;
	export let columnValue;

	let squareId = undefined;

	// Not a good solution? Alternative would be to turn matrix items into objects and populate with id, which has similar scalability to this solution
	// if (rowValue === 0) {
	// 	squareId = columnValue + 1;
	// } else if (rowValue === 1) {
	// 	squareId = columnValue + 4;
	// } else {
	// 	squareId = columnValue + 7;
	// }

	if (rowValue === 0) {
		squareId = columnValue;
	} else if (rowValue === 1) {
		squareId = columnValue + 3;
	} else {
		squareId = columnValue + 6;
	}

	// $: console.log(rowValue, columnValue);

	const dispatch = createEventDispatcher();

	function userClick() {
		dispatch('message', {
			squareId: squareId
		});
	}
</script>

<!-- Needs to respond to reset game -->
<div on:click|once={userClick}>
	{#if squareValue}
		<i class="fas fa-times fa-3x"></i>
	{:else if squareValue === false}
		<i class="far fa-circle fa-3x"></i>
	{:else}
		<h3>#</h3>
	{/if}
</div>

<style>
	div {
		cursor: pointer;
	}
</style>