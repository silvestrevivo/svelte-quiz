<script>
  import { fade, blur, fly, slide, scale } from "svelte/transition";
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();
  let w;
  // $: console.log("width of modal", w);
  //this width is going to change dynamically if we resize
</script>

<style lang="scss">
  .modal-bg {
    position: fixed;
    top: 0;
    right: 0;
    left: 0;
    bottom: 0;
    padding: 15px;
    background: rgba(0, 0, 0, 0.6);
    .modal {
      background: #fff;
      padding: 20px;
      border-radius: 15px;
    }
  }
</style>

<div class="modal-bg " transition:fade bind:clientWidth={w}>
  <div class="modal" transition:fly={{ y: -100 }}>
    <button on:click={() => dispatch('close')}>Close</button>
    <slot />
  </div>
</div>
