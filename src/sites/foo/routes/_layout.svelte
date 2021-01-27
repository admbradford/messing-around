<script>
	import Nav from '../../../global/components/Nav.svelte';
	import HeaderMenu from '../components/HeaderMenu.svelte';
	export let segment;
</script>

<style>
	main {
		position: relative;
		max-width: 56em;
		background-color: white;
		padding: 2em;
		margin: 0 auto;
		box-sizing: border-box;
	}
</style>

<Nav>
	<HeaderMenu {segment} />
</Nav>

<main>
	<slot></slot>
</main>