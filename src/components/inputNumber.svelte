<script>
  export let placeholder = "Digite um número";
  export let name;
  export let label;
  export let valor = 0;
  export let onInput;

  function handleInput(event) {
    valor = event.target.value; // Atualiza o valor local
    if (onInput) {
      onInput(valor); // Chama o evento de input se fornecido
    }
  }
</script>

<div class="container-input">
  <label for={name}>{label}</label>
  <input placeholder={placeholder} max={5}  bind:value={valor} on:input={handleInput} type="number" {name} id={name} />
</div>

<style>
  input {
    padding: 8px;
    border: 2px solid #353535;
    border-radius: 8px;
  }

  .container-input {
    display: flex;
    flex-direction: column;
    gap: 3px;
    padding: 10px;
    color: #353535;
  }
</style>
