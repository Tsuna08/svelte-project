<script>
	let name = 'world'
	const buttons = ['AC', '', '%', '/', '7', '8', '9', 'X', '4', '5', '6', '-', '1', '2', '3', '+', '()', '0', ',', '=']
	function handleClick(event) {
		console.log('event: ', event)
		alert('no more alerts')
	}
</script>

<div class="container">
	<div class="top">
		<!-- <button class="history">',
		<button  class="delete">', -->
	</div>

	<ul class="historyDetails">
		<li>
			<small />
			<h2>h2</h2>
		</li>
	</ul>

	<div class="middle">
		<small />
		<div>
			<h1>Hello {name}!</h1>
		</div>
	</div>
	<div class="bottom">
		{#each buttons as button}
			<button on:click={handleClick}>{button}</button>
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
</style>
