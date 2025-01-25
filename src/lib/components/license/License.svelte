<script>
  import { window_closed } from "$lib/store/store"
  import { slide } from "svelte-legos"
  import { quartOut } from "svelte/easing"

  export let intro_ended = false

  let web_license = "4Saken Rf. | Website by Noir | Template by Ravimo"
  let art_license = "4Saken Rf. | Artwork by Noir"
  
</script>

{#if intro_ended}
<div class="absolute flex-middle items-end h-screen w-screen pointer-events-none
            {$window_closed ? "max-lg:items-start" : ""}">

  <p3 class="text-white m-3"
  transition:slide = {
    {
      direction: "bottom",
      easing: quartOut,
      duration: 500}
  }>{$window_closed ? art_license : web_license}</p3>
</div>
{/if}