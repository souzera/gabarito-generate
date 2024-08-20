<script>
    import Bubble from "../components/bubble.svelte";
    export let numero;
    export let qtd_opcoes=5;

    let alfabeto = ["a", "b", "c", "d", "e", 'f', "g", "h", "j"]

    let opcoes = alfabeto.slice(0, qtd_opcoes)
    console.log(opcoes)
</script>

<div class="line">
    <span>{numero}</span>
    {#each opcoes as opcao}
        <Bubble value={opcao}/>
    {/each}
</div>

<style>
    .line{
        display: flex;
        justify-content: center;
        align-items: center;
        gap: 8px;
        padding: 4px 8px;
        border: 2px solid #353535;
        border-radius: 12px;
    }
</style>