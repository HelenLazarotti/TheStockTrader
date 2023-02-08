<template>
    <v-toolbar app id="navbar">
        <v-toolbar-title class="logotipo">
            <span id="stock">Stock</span>
            <span id="trader" class="font-weight-light">Trader</span>
        </v-toolbar-title>
        <v-toolbar-items>
            <v-btn flat to="/">Início</v-btn>
            <v-btn flat to="/portfolio">Portfólio</v-btn>
            <v-btn flat to="/stocks">Ações</v-btn>
        </v-toolbar-items>

        <v-spacer></v-spacer>

        <v-toolbar-items>
            <v-btn flat @click="endDay">Finalizar Dia</v-btn>
            <v-menu offset-y>
                <v-btn flat slot="activator">Salvar & Carregar</v-btn>
                <v-list>
                    <v-list-tile @click="saveData">
                        <v-list-tile-title>Salvar Dados</v-list-tile-title>
                    </v-list-tile>
                    <v-list-tile @click="loadDataLocal">
                        <v-list-tile-title>Carregar Dados</v-list-tile-title>
                    </v-list-tile>
                </v-list>
            </v-menu>
            <v-layout align-center>
                <span class="text-uppercase grey--text text--darken-2">
                    Saldo: {{ funds | currency }}
                </span>
            </v-layout>
        </v-toolbar-items>
    </v-toolbar>
</template>

<script>
import { mapActions } from 'vuex'

export default {
    computed: {
        funds() {
            return this.$store.getters.funds
        }
    },
    methods: {
        ...mapActions(['randomizeStocks', 'loadData']),
        endDay() {
            this.randomizeStocks()
        },
        saveData() {
            const { funds, stockPortfolio, stocks } = this.$store.getters
            this.$http.put('data.json', { funds, stockPortfolio, stocks })
        },
        loadDataLocal() {
            this.loadData()
        }
    }
}
</script>

<style>
    #navbar{
        background-color: #cfcece;
    }
    .logotipo{
        font-size: 25px;
        filter: drop-shadow(3px 3px 2px #8a8a8a);
        margin-right: 1em;
    }
    #stock {
        color: #ec2d70;
    }
    #trader {
         color: #e89a25;
    }
</style>
