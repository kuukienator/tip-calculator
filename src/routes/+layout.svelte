<script>
	import './styles.css';
</script>

<div class="app">
	<header><h1>Tip Calculator</h1></header>
	<main>
		<slot />
	</main>
	<footer>
		<a href="https://twitter.com/kuukienator" target="_blank" rel="noreferrer">@kuukienator</a>
		<span>2023</span>
	</footer>
</div>

<style>
	.app {
		display: flex;
		flex-direction: column;
		min-height: 100vh;
	}

	h1 {
		font-size: 2.5rem;
		padding: 0;
		margin: 0;
	}

	main {
		flex: 1;
		display: flex;
		flex-direction: column;
		padding: 3rem 1rem;
		width: 100%;
		max-width: 64rem;
		margin: 0 auto;
		box-sizing: border-box;
	}

	header,
	footer {
		display: flex;
		flex-direction: row;
		justify-content: center;
		align-items: center;
		padding: 1rem;
		background: #010001;
		gap: 0.5rem;
	}

	a {
		color: #fefefe;
	}
</style>
