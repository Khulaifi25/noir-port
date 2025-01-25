<script>
  export var title = ""
  var head_div = null
  
  $:{
    if (title != "" && head_div != null){
      head_div.classList.add('gap-4')
    }
  }
</script>

<div class="relative flex-middle" bind:this={head_div}>
  <div class="flex-middle ms-[20px]">
    <div class="opacity-30 bg-[--theme-white] h-[2px] w-full"/>
  </div>
  <h3 class="leading-none">{title}</h3>
  <div class="flex-middle me-[20px]">
    <div class="opacity-30 bg-[--theme-white] h-[2px] w-full"/>
      </div>
</div>