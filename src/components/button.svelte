<script>
  export let child;
  export let onClick;
  export let hasImage = false;
</script>

<button type="button" on:click={onClick}>
  {#if !hasImage}
    {child}
  {/if}
  {#if hasImage}
    <img src={child} alt="image-button">
  {/if}
</button>

<style>
  button {
    width: fit-content;
    height: fit-content;
    padding: 10px;
    border: 3px solid #353535;
    border-radius: 10px;
    background-color: transparent;
    font-family: "Cascadia Code", sans-serif;
    font-size: 1.3rem;
    color: #353535;
    transition: all 0.5s ease-in;
    cursor: pointer;
  }

  button:hover {
    scale: 1.1;
  }

  img{
    height: 32px;
  }
</style>
