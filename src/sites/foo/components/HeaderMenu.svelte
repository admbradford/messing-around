<script>
	export let segment;
	export const menuItems = [
		{
			href: '.',
			text: 'Home',
		},
		{
			segment: 'about',
			href: 'about',
			text: 'About',
		},
		{
			segment: 'cats',
			href: 'cats',
			text: 'Cats',
    },
    {
			segment: 'dogs',
			href: 'dogs',
			text: 'Dogs',
    },
    {
			segment: 'birds',
			href: 'birds',
			text: 'Birds',
		},
	]
</script>

<style lang="scss">
  @import "../../../global/styles/mixins.scss";
	@include main-nav;
</style>

<ul>
  {#each menuItems as menuItem}
    <li>
      <a aria-current="{segment === menuItem.segment ? 'page' : undefined}" href="{menuItem.href}">
        {menuItem.text}
      </a>
    </li>
  {/each}
</ul>
