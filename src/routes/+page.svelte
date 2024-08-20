<script>
    import InputNumber from "../components/inputNumber.svelte";
    import Button from "../components/button.svelte";
    import Line from "../components/line.svelte";
    import html2canvas from "html2canvas";

    let questoes = 1
    let opcoes = 5

    let colunas = 1

    let array = [{questao: questoes, opcoes: opcoes}]

    function handleQuestoes(novovalor){
        questoes = novovalor
    }

    function handleOpcoes(novovalor){
        opcoes = novovalor
    }

    function load(){

        colunas = Math.floor(questoes/10)
        if (questoes%10 != 0) colunas += 1

        array = []
        for( let i = 0; i < questoes; i++){
            array.push({questao: (i+1).toString().padStart(2, "0"), opcoes: opcoes})
        }
    }

    async function downloadAsImage(){
        const element = document.querySelector('.gabarito-container');
        const canvas = await html2canvas(element)

        const data = canvas.toDataURL(`image/png`)
        const link = document.createElement("a")
        link.href = data
        link.download = `gabarito-${Date.now().toString()}.png`
        document.body.appendChild(link)
        link.click();
        document.body.removeChild(link)
    }
</script>

<main>

    <header>
        <div>
            <h2>Gerador Gabarito</h2>
            <p>Escolha a quantidade de questões e opções</p>
        </div>

        <div class="baixar-container">
            <Button child={'/baixar.png'} hasImage onClick={downloadAsImage}/>
        </div>
    </header>

    <div class="form-group">
        <InputNumber onInput={handleQuestoes} valor={questoes} label="Número de Questões" name="n_qst"/>
        <InputNumber onInput={handleOpcoes} valor={opcoes} label="Qtd. de Opções" name="qtd_op"/>
        <Button onClick={load} child="Ok"/>
    </div>

    <div class="gabarito-container" style="--colunas:{colunas};">
        {#each array as qst_config}
            <Line numero={qst_config['questao']} qtd_opcoes={qst_config['opcoes']}/>
        {/each}
    </div>


</main>

<style>
    main{
        display: flex;
        justify-content: start;
        align-items: center;
        flex-direction: column;
        margin-top: 10px;
        gap: 10px;
        height: 100vh;
        width: 100%;
    }

    header{
        display: flex;
        align-items: center;
        justify-content: space-between;
        gap: 30px;
    }

    .form-group{
        display: flex;
        justify-content: center;
        align-items: center;
        background-color: lightgray;
        border: 3px solid #353535;
        border-radius: 10px;
        padding: 10px;
        gap: 5px;
    }

    .gabarito-container{
        display: grid;
        grid-template-columns: repeat(var(--colunas), 1fr);
        grid-template-rows: auto;
        gap: 10px;
        padding:30px;
        background-color: transparent;
    }

    .baixar-container{
        display: flex;
        align-items: center;
        justify-content: center;
        height: 100%;
    }
</style>