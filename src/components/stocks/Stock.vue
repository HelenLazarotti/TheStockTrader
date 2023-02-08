<template>
    <v-flex class="pr-3 pb-3" xs12 md6 lg4>
        <v-card id="card-actions">
            <v-card-title class="headline">
                <strong>{{ stock.name }} <small>(Preço: {{ stock.price | currency }})</small></strong>
            </v-card-title>
        </v-card>
        <v-card id="card-infos">
            <v-container fill-height>
                <v-text-field label="Quantidade" type="number"
                    :error="insufficientFunds || !Number.isInteger(quantity)"
                    v-model.number="quantity" />
                <v-btn class="green white--text"
                    :disabled="insufficientFunds || quantity <= 0 || !Number.isInteger(quantity)"
                    @click="buyStock">{{ insufficientFunds ? 'Insuficiente' : 'Comprar' }}</v-btn>
            </v-container>
        </v-card>
    </v-flex>
</template>

<script>
export default {
    props: ['stock'],
    data() {
        return {
            quantity: 0
        }
    },
    computed: {
        funds() {
            return this.$store.getters.funds
        },
        insufficientFunds() {
            return this.quantity * this.stock.price > this.funds
        }
    },
    methods: {
        buyStock() {
            const order = {
                stockId: this.stock.id,
                stockPrice: this.stock.price,
                quantity: this.quantity
            }
            this.$store.dispatch('buyStock', order)
            this.quantity = 0
        }
    }
}
</script>

<style>
    #card-actions{
        background-color: #ec2d70;
        color: #fff;
        border-top-left-radius: 1em;
        border-top-right-radius: 1em;
        margin-top: 2em;
    }
    #card-infos{
        background-color: #ececec;
        border-bottom-left-radius: 1em;
    }
</style>
