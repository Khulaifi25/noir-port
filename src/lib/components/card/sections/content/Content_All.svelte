<script>
  import { window_element } from "$lib/store/store.js";
  import { onMount } from "svelte";
  let this_element = null;
  let back_button = null;

  onMount(() => {
    if (this_element === null) return;
    $window_element.scroll({
      top: 1000,
      behavior: "smooth"
    });
  });

  function scrollToTop() {
    $window_element.scroll({
      top: 0,
      behavior: "smooth"
    });
  }
</script>

<a class="mr-5" href="https://vgen.co/noirs_rf" target="_blank" bind:this={this_element}>
  <button class="button-theme group">
    <p1 class="color-[--theme--white] group-hover:text-[--theme-black]">
      Click Here !
    </p1>
  </button>
</a>

<button class="button-theme group" on:click={scrollToTop} bind:this={back_button}>
  <p1 class="color-[--theme--white] group-hover:text-[--theme-black]">
    ↑ Back to Top
  </p1>
</button>