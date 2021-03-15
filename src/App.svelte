<script>
	import Square from './components/Square.svelte';

	let matrix = [
		[null, null, null],
		[null, null, null],
		[null, null, null]
	];

	let xTurn = true;

	let winner = null;

	// x = true
	// o = false

	function handleClick(event) {
		let squareId = event.detail.squareId;
		let row = Math.floor(squareId / 3);
		let column = squareId % 3;
		xTurn ? matrix[row][column] = true : matrix[row][column] = false;
		xTurn = !xTurn;
		matrix = matrix;
	}

	$: horizontal1 = matrix[0][0] + matrix[0][1] + matrix[0][2];
	$: horizontal2 = matrix[1][0] + matrix[1][1] + matrix[1][2];
	$: horizontal3 = matrix[2][0] + matrix[2][1] + matrix[2][2];
	$: vertical1 = matrix[0][0] + matrix[1][0] + matrix[2][0];
	$: vertical2 = matrix[0][1] + matrix[1][1] + matrix[2][1];
	$: vertical3 = matrix[0][2] + matrix[1][2] + matrix[2][2];
	$: diagonalDown = matrix[0][0] + matrix[1][1] + matrix[2][2];
	$: diagonalUp = matrix[2][0] + matrix[1][1] + matrix[0][2];

	$: winner =
		horizontal1 > 2 ?
			true :
		horizontal2 > 2 ?
			true :
		horizontal3 > 2 ?
			true :
		vertical1 > 2 ?
			true :
		vertical2 > 2 ?
			true :
		vertical3 > 2 ?
			true :
		diagonalUp > 2 ?
			true :
		diagonalDown > 2 ?
			true :
		horizontal1 < -2 ?
			false :
		horizontal2 < -2 ?
			false :
		horizontal3 < -2 ?
			false :
		vertical1 < -2 ?
			false :
		vertical2 < -2 ?
			false :
		vertical3 < -2 ?
			false :
		diagonalUp < -2 ?
			false :
		diagonalDown < -2 ?
			false :
		null;

	function resetGame() {
		matrix = matrix.map(subarray => subarray.map(item => null));
	}
</script>

<svelte:head>
	<link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.7.2/css/all.css" integrity="sha384-fnmOCqbTlWIlj8LyTjo7mOUStjsKC4pOpQbqyi7RrhN7udi9RwhKkMHpvLbHG9Sr" crossorigin="anonymous">
</svelte:head>

<main>
	<h1>Tic Tac Toe!</h1>
	{#if winner}
		<h2>Player {winner ? 'X' : 'Y'} wins!</h2>
	{/if}
	<div>
		{#each matrix as row, i}
			{#each row as item, j}
				<Square on:message={handleClick} squareValue={item} rowValue={i} columnValue={j}/>
			{/each}
		{/each}
	</div>
	<button on:click={resetGame}>Start over</button>
</main>

<style>
	main {
		height: 100vh;
		display: flex;
		flex-flow: column nowrap;
		justify-content: center;
		align-items: center;
	}

	h1 {
		font-size: 5em;
	}

	div {
		width: 30%;
		height: 30%;
		padding: 1em;
		display: grid;
		grid-template-columns: repeat(3, 1fr);
		grid-template-rows: repeat(3, 1fr);
		gap: 1em;
		justify-items: center;
		align-items: center;
	}
</style>