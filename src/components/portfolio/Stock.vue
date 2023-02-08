<template>
    <v-flex class="pr-3 pb-3" xs12 md6 lg4>
        <v-card id="card-portfolio">
            <v-card-title class="headline">
                <strong>
                    {{ stock.name }}
                    <small>
                        (Preço: {{ stock.price | currency }} | Qtde: {{ stock.quantity }})
                    </small>
                </strong>
            </v-card-title>
        </v-card>
        <v-card  id="card-infos">
            <v-container fill-height>
                <v-text-field label="Quantidade" type="number"
                    :error="insufficientQuantity || !Number.isInteger(quantity)"
                    v-model.number="quantity" />
                <v-btn class="info white--text"
                    :disabled="insufficientQuantity || quantity <= 0 || !Number.isInteger(quantity)"
                    @click="sellStock">{{ insufficientQuantity ? 'Insuficiente' : 'Vender' }}</v-btn>
            </v-container>
        </v-card>
    </v-flex>
</template>

<script>
import { mapActions } from 'vuex'

export default {
    props: ['stock'],
    data() {
        return {
            quantity: 0
        }
    },
    computed: {
        insufficientQuantity() {
            return this.quantity > this.stock.quantity
        }
    },
    methods: {
        ...mapActions({ sellStockAction: 'sellStock' }),
        sellStock() {
            const order = {
                stockId: this.stock.id,
                stockPrice: this.stock.price,
                quantity: this.quantity
            }
            this.sellStockAction(order)
            // this.$store.dispatch('sellStock', order)
            this.quantity = 0
        }
    }
}
</script>

<style>
 #card-portfolio{
        background-color: #e89a25;
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
