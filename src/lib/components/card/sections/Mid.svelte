<script>
  import Tide from "$lib/etc/tide.svelte"
  import { nav_list, window_controls } from "$lib/etc/nav_and_links.svelte"
  import { toggle_about, toggle_portfolio, toggle_commission, toggle_contact } from "$lib/store/store.js"
  import { can_maximize, window_closed } from "$lib/store/store";
  import { links } from "$lib/etc/nav_and_links.svelte"

  export let h_full = false
  export let main_window = null

  let toggles = [toggle_about, toggle_portfolio, toggle_commission, toggle_contact]
  let last_button = null

  function h_full_false(){
    setTimeout(()=>{
      h_full = false
    }, 500)
  }

  function toggle_nav(txt){
    if (main_window === null) return
    
    // Presist window maximize when clicked outside the commission
    if($toggle_commission) main_window.return_to_last_maximize()
    // Enable maximize
    $can_maximize = true
    // Set all to false
    toggles.forEach((t) => {t.set(false)})
    nav_list.forEach((n) => {
      document.getElementById(`nav-${n.text}`).classList.remove("activated")
      document.getElementById(`txt-${n.text}`).classList.remove("txt-activated")
    })
    
    // For turning off button from previously clicked button
    if (last_button === txt && h_full === true) {h_full_false(); return}

    last_button = txt
    h_full = true

    // Set current selected nav to be highlighted
    document.getElementById(`nav-${txt}`).classList.add("activated")
    document.getElementById(`txt-${txt}`).classList.add("txt-activated")

    // Manage toggles
    switch (txt){
      case "About":
        $toggle_about = true
        break
      case "Portfolio":
        $toggle_portfolio = true
        // temporary
        main_window.toggle_window(true)
        document.getElementById(`nav-${txt}`).classList.remove("activated")
        document.getElementById(`txt-${txt}`).classList.remove("txt-activated")
        break
      case "Commission":
        $toggle_commission = true
        break
      case "Contact":
        $toggle_contact = true
        break
    }
  }

</script>

<div class="relative flex-middle flex-col items-start gap-2 h-auto my-10">
  <!---------------------- Mid Line ---------------------->
  <Tide />
  <!---------------------- Nav Section ---------------------->
  <div class="flex-middle gap-4 my-7">
    {#each nav_list as nav}
      <!-- <a href={nav.link} target="_blank"> -->
        <button class="button-theme group"
                id="nav-{nav.text}"
                on:click={() => {toggle_nav(nav.text)}}>
          <p1 id="txt-{nav.text}" class="group-hover:text-[--theme-black]">{nav.text}</p1>
        </button>
      <!-- </a> -->
    {/each}
  </div>
  <!-- Links list -->
  <div class="flex-middle flex-row mt-20 gap-2 max-sm:gap-0">
    {#each links as link}
      <a href={link.link} target="_blank" class="group hover:bg-[--theme-white] hover:glow">
        <div class="flex-middle group-hover:bg-[--theme-white]">
          <i class={link.icon + " text-3xl px-2 group-hover:text-[--theme-black]"}/>  
          <p3 class=" absolute translate-y-6 text-transparent duration-200 group-hover:text-[--theme-white]
                      group-hover:translate-y-9
                      max-sm:group-hover:translate-y-7">{link.name}</p3>
        </div>
      </a>
    {/each}

  </div>
  <!--
  <div class="flex-middle min-h-10"/>-->
</div>

<style>
  :global(.activated){
    @apply bg-[--theme-white] border-[--theme-white]
  }

  :global(.txt-activated){
    @apply text-[--theme-black]
  }
</style>