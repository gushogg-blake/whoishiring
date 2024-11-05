<script lang="ts">
  export let disabled = false;
  export let click = () => {};
  export let active = false;
  export let exclude = false;
</script>


<button
  class:active
  class:exclude
  class:disabled
  on:click={() => click()}
  disabled={disabled}
>
  <slot></slot>
</button>

<style>
  button {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 1em;

    font-family: 'Mulish', sans-serif;
    font-size: 1em;
    padding: 0.8em 1em;

    border: 1px solid #231F20;
    border-radius: 1em;

    color: #231F20;
    background-color: #F9F5EB;
  }

  button:hover:not(.disabled) {
    cursor: pointer;
  }

  .active {
    color: #F9F5EB;
    background-color: #4E7539;
  }

  .exclude {
    color: #F9F5EB;
    background-color: #7C1010;
  }

  .disabled {
    opacity: 0.5;
  }
</style>
