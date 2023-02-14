<script>
	import { create, all } from 'mathjs'

	let currentValue = '0'
	let curentResult = ''
	let prevValue = ''
	let prevResult = ''
	let historyData = []
	const buttons = [
		{ name: 'C', type: 'button' },
		{ name: '', type: 'deleteButton' },
		{ name: '%', type: 'button' },
		{ name: '/', type: 'button' },
		{ name: '7', type: 'number' },
		{ name: '8', type: 'number' },
		{ name: '9', type: 'number' },
		{ name: 'x', type: 'button' },
		{ name: '4', type: 'number' },
		{ name: '5', type: 'number' },
		{ name: '6', type: 'number' },
		{ name: '-', type: 'button' },
		{ name: '1', type: 'number' },
		{ name: '2', type: 'number' },
		{ name: '3', type: 'number' },
		{ name: '+', type: 'button' },
		{ name: '+/-', type: 'number' },
		{ name: '0', type: 'number' },
		{ name: '.', type: 'symbol' },
		{ name: '=', type: 'button' }
		// 'C',
		// 'CE',
		// '%',
		// '/',
		// '7',
		// '8',
		// '9',
		// 'x',
		// '4',
		// '5',
		// '6',
		// '-',
		// '1',
		// '2',
		// '3',
		// '+',
		// '+/-',
		// '0',
		// '.',
		// '='
	]
	const math = create(all, {})

	function handleClick(event) {
		if (event.target.value.toString().match(/=/)) {
			// ;[curentResult, currentValue] = [currentValue, curentResult]
			historyData.push({
				operations: currentValue,
				sum: curentResult
			})
			console.log('historyData: ', historyData)
			prevValue = currentValue
			prevResult = prevResult
			;[curentResult, currentValue] = [currentValue, curentResult]
			prevValue = currentValue
			prevResult = prevResult
		} else if (event.target.value === 'C') {
			currentValue = '0'
		} else if (event.target.value === '') {
			currentValue = currentValue.length > 1 ? currentValue.slice(0, -1) : '0'
			calculate()
		} else {
			appendNumber(event.target.value)
			calculate()
		}
	}

	const calculate = () => {
		try {
			// Math.trunc используется для округления до целого числа
			curentResult = `=${math.evaluate(currentValue)}`
		} catch {
			curentResult = 'Error'
			// // сохраняем значение поля
			// let oldValue = output.textContent
			// // создаем новую переменную
			// let newValue = 'недопустимое выражение'
			// // выводим значение новой переменной в поле
			// output.textContent = newValue
			// // через полторы секунды возвращаем полю старое значение
			// setTimeout(() => {
			// 	output.textContent = oldValue
			// }, 1500)
		}
	}

	const appendNumber = (value) => {
		currentValue = currentValue === '0' ? value : currentValue + value
	}
</script>

<div class="container">
	<ul class="historyDetails">
		{#each historyData as history}
			<li>
				<small>{history.operations}</small>
				<h2>{history.sum}</h2>
			</li>
		{/each}
	</ul>
	<div>32423 {historyData}</div>
	<div class="middle">
		<small />
		<div>
			<h1>{currentValue}</h1>
		</div>
	</div>
	<div class="bottom">
		{#each buttons as button}
			<button on:click={handleClick} name="key" class={button.type} value={button.name} aria-label={button.name}>
				{button.name}
			</button>
		{/each}
	</div>
</div>

<style>
	.container {
		width: 100%;
		height: 100%;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		gap: 1rem;
		flex: 1;
	}
	.bottom {
		display: grid;
		grid-template-columns: repeat(4, 50px);
		grid-gap: 5px;
	}
	button {
		height: 50px;
		width: 50px;
		border-radius: 50%;
		border: none;
	}
	.deleteButton {
		background: url('../assets/delete.svg') no-repeat top left;
		background-color: rgb(239, 239, 239);
	}
</style>
