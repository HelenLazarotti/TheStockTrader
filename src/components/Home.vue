<template>
    <div>
        <h1 class="title-h1">Negocie e Consulte suas Ações</h1>

        <v-sheet id="box-save-load" class="mb-4">
            <v-icon class="white--text mr-3">info</v-icon>
            <span class="span-save">
                Você pode Salvar & Carregar os Dados
            </span>
        </v-sheet>

        <v-sheet id="box-end-day">
            <v-icon class="white--text mr-3">info</v-icon>
            <span class="span-save">
                Clique em 'Finalizar Dia' para iniciar um novo dia!
            </span>
        </v-sheet>

        <v-divider class="v-divider"/>

        <p class="my-sold"><strong>Seu Saldo:</strong> {{ funds | currency }}</p>
    </div>
</template>

<script>
export default {
    computed: {
        funds() {
            return this.$store.getters.funds
        }
    }
}
</script>

<style>
    .title-h1 {
        font-size: 40px;
        text-align: center;
        margin: 1em 1em;
        font-weight: 200;
    }
    #box-save-load, #box-end-day{
        padding: 1em;
        display: flex;
        align-items: center;
        border-radius: 2em;
    }
    #box-save-load{
        background-color: #ec2d70;
    }
    #box-end-day{
        background-color: #e89a25;
    }
    .span-save {
        color: #fff;
        font-size: 20px;
        font-weight: 300;
    }
    .v-divider{
        background-color: wheat;
        margin-top: 3em;
        margin-bottom: 3em;
    }
    .my-sold{
        font-size: 30px;
        font-weight: 300;
        color: #d3d3d3;
    }
</style>
