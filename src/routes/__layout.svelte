<script>
	import Nav from '$lib/Nav.svelte'
</script>

<div class="container">
	<Nav />
	<slot />
</div>

<style>
	@import url('https://fonts.googleapis.com/css2?family=Roboto+Serif:wght@400;700&display=swap');

	* {
		font-family: 'Roboto Serif', sans-serif;
	}

	.container {
		max-width: 800px;
		margin: 50px auto;
	}
</style>
