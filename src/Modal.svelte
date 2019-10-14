<script>
  import { fade, blur, fly, slide, scale } from "svelte/transition";
</script>

<style>
  .modal-bg {
    position: fixed;
    top: 0;
    right: 0;
    left: 0;
    bottom: 0;
    padding: 15px;
    background: rgba(0, 0, 0, 0.6);
  }

  .modal {
    background: #fff;
    padding: 20px;
    border-radius: 15px;
  }
</style>

<div class="modal-bg " transition:fade>
  <div class="modal" transition:fly={{ y: -100 }}>
    <slot />
  </div>
</div>
