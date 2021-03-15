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

	function checkForWinner(mtx) {
		// Eight possible winning combinations
		// Also check if all squares full and no winner
		// x will always fill one more square than o if game completed
		// Check horizontally: add or subtract 1 for each bool, if end of row has +3/-3 there is a winner
		// - Binomial walk
		// Use a tree/graph to navigate through possible outcomes: if [0][0] is true/false, go down that branch, etc
		// - Alternative: iterating over the matrix 8 times, which becomes computationally infeasible as the matrix grows
		// 				   root
		// 			true		 false
		// 		true	false  true  false
		// Leaves will have results, whether they are winning, tie-ing, or incomplete scenarios
		// Count number of turns, since the minimum number of turns needed to win is three
		// - Count total number of turns, which would result in five being the minimum number of turns to win
		// What direction to go in if null node?
		// Can't have tree expand to account for every possible permutation of the matrix

		// WINNING COMBO WILL ALWAYS BE A PRODUCT OF 3 IF ITEMS ARE 1-3 IN EACH SUBARRAY

		// let totalCount = 0;
		// for (let i = 0; i < mtx.length; i++) {
		// 	for (let j = 0; j < mtx[i].length; j++) {
		// 		if (mtx[i][j] === false) {
		// 			totalCount--;
		// 		} else if (mtx[i][j] === true) {
		// 			totalCount++;
		// 		}
		// 	}
		// 	if (totalCount === 3) {
		// 		return 'x wins';
		// 	} else if (totalCount === -3) {
		// 		return 'o wins';
		// 	}
		// }

		// if (mtx[0]) {
		// 	if (mtx[1])
		// } else if (!mtx[0] && mtx[0] !== null) {
			
		// }

		// if (mtx[0][0] && mtx[0][1] && mtx[0][2]) {
		// 	// winner
		// } else if (mtx[0][0] && mtx[1][2] && mtx[2][3]) {
		// 	// winner
		// }

		// let xScore = undefined;
		// let oScore = undefined;
		// for (let i = 0; i < mtx.length; i++) {
		// 	xScore = 0;
		// 	oScore = 0;
		// 	for (let j = 0; j < mtx[i].length; j++) {
		// 		// if (mtx[i][j]) {
		// 		// 	xScore += j + 1;
		// 		// } else if 
		// 		// mtx[i][j] ? xScore++ : oScore++ ?? null;
		// 		// mtx[i][j] === null ? null : mtx[i][j] ? xScore++ : oScore++;
		// 		mtx[i][j] ? oScore += j + 1 : mtx[i][j] !== null ? oScore += j + 1 : null;
		// 	}
		// 	// if (xScore)
		// }

		// const optionArr = [];
		// let option;
		// // Horizontal straight
		// for (let i = 0; i < mtx.length; i++) {
		// 	option = 0;
		// 	for (let j = 0; j < mtx[i].length; j++) {
		// 		mtx[i][j] ? option += j + 1 : mtx[i][j] !== null ? option -= j + 1 : null;
		// 	}
		// 	optionArr.push(option);
		// }

		// // Vertical straight
		// for (let i = 0; i < mtx.length; i++) {
		// 	option = 0;
		// 	for (let j = 0; j < mtx.length; j++) {
		// 		mtx[j][i] ? option += i + 1 : mtx[j][i] !== null ? option -= i + 1 : null;
		// 	}
		// 	optionArr.push(option);
		// }

		// option = 0;
		// for (let i = 0; i < mtx.length; i++) {
		// 	mtx[i][i] ? option += i + 1 : mtx[i][i] !== null ? option -= i + 1 : null;
		// }
		// optionArr.push(option);

		// option = 0;
		// for (let i = mtx.length - 1; i >= 0; i--) {
		// 	mtx[i][i] ? option += i + 1 : mtx[i][i] !== null ? option -= i + 1 : null;
		// }
		// optionArr.push(option);
		
		// // const winnerArr = optionArr.filter(num => Math.abs(num) % 3 === 0 && num !== 0 && num > 3);
		// const winnerArr = optionArr.filter(num => Math.abs(num) === 6 || Math.abs(num) === 9);

		// console.log(winnerArr);
		// if (winnerArr[0] > 0) {
		// 	winner = 'X';
		// } else if (winnerArr[0] < 0) {
		// 	winner = 'O';
		// }

		// const winScenarios = {
		// 	horizontal1: 0,
		// 	horizontal2: 0,
		// 	horizontal3: 0,
		// 	vertical1: 0,
		// 	vertical2: 0,
		// 	vertical3: 0,
		// 	diagonalRight: 0,
		// 	diagonalLeft: 0
		// };
		// for (let i = 0; i < mtx.length; i++) {
		// 	for (let j = 0; j < mtx[i].length; j++) {

		// 	}
		// }

		// Create bound win scenario vars that increment or decrement based on the square clicked

	}

	// $: checkForWinner(matrix);

	$: horizontal1 = matrix[0][0] + matrix[0][1] + matrix[0][2];
	$: horizontal2 = matrix[1][0] + matrix[1][1] + matrix[1][2];
	$: horizontal3 = matrix[2][0] + matrix[2][1] + matrix[2][2];
	$: vertical1 = matrix[0][0] + matrix[1][0] + matrix[2][0];
	$: vertical2 = matrix[0][1] + matrix[1][1] + matrix[2][1];
	$: vertical3 = matrix[0][2] + matrix[1][2] + matrix[2][2];
	$: diagonalDown = matrix[0][0] + matrix[1][1] + matrix[2][2];
	$: diagonalUp = matrix[2][0] + matrix[1][1] + matrix[0][2];

	$: console.log(horizontal1);

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
		

	function handleClick(event) {
		let squareId = event.detail.squareId;
		let row = Math.floor(squareId / 3);
		let column = squareId % 3;
		// let column = squareId - (row * 3);
		// console.log(row, column);

		// squareId % 3 = squareId - (row * 3)

		xTurn ? matrix[row][column] = true : matrix[row][column] = false;
		xTurn = !xTurn;
		matrix = matrix;
	}

	function resetGame() {
		matrix = matrix.map(subarray => subarray.map(item => null));
	}

	$: console.log(matrix);
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
		/* margin-top: 0; */
		/* margin: 0; */
		/* margin-bottom: 1em; */
		font-size: 5em;
		/* flex: .5; */
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
		/* justify-items: stretch; */
		align-items: center;
		/* align-items: stretch; */
		/* background-color: green; */
	}
</style>