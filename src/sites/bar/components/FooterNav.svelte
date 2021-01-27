<script>
  export let menuItems;
  export let segment;
</script>

<style lang="scss">
  @import "../../../global/styles/mixins.scss";
  @include main-nav;
  
  nav {
    border: solid 1px #000;
  }
</style>

<nav>
  <ul>
    {#each menuItems as menuItem}
      <li>
        <a aria-current="{segment === menuItem.segment ? 'page' : undefined}" href="{menuItem.href}">
          {menuItem.text}
        </a>
      </li>
    {/each}
  </ul>  
</nav>