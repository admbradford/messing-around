<script>
	import Nav from '@/components/Nav.svelte';
	import FooterNav from '../components/FooterNav.svelte';
	export let segment;
	export const menuItems = [
		{
			href: '.',
			text: 'BAR HOME',
		},
		{
			segment: 'about',
			href: 'about',
			text: 'BAR ABOUT',
		},
		{
			segment: 'blog',
			href: 'blog',
			text: 'BAR BLOG',
		},
	]
</script>

<style lang="scss">
	@import "../../../global/styles/mixins.scss";
	@include main-nav;
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
	<ul>
		{#each menuItems as menuItem}
			<li>
				<a aria-current="{segment === menuItem.segment ? 'page' : undefined}" href="{menuItem.href}">
					{menuItem.text}
				</a>
			</li>
		{/each}
	</ul>
</Nav>

<main>
	<slot></slot>
</main>

<footer>
	<FooterNav {menuItems} {segment} />
</footer>