<template>
    <v-container>
        <v-layout justify-center>
            <div class="cart pt-10">
                <h2>Your Cart</h2>
                <p v-show="!cartProducts.length">
                    <i>Please add some products to cart.</i>
                </p>
                <ul>
                    <li
                        v-for="product in cartProducts"
                        :key="product.id"
                    >{{product.title}} - {{product.price}} × {{product.quantity}}</li>
                </ul>
                <v-card class="red--text text--darken-4 mb-5">Total: {{cartTotalPrice}}</v-card>
                <p>
                    <v-btn
                        outlined
                        rounded
                        class="blue lighten-3"
                        :disabled="!cartProducts.length"
                        @click="checkout(cartProducts)"
                    >Checkout</v-btn>
                </p>
                <p v-show="checkoutStatus">Checkout {{checkoutStatus}}.</p>
            </div>
        </v-layout>
    </v-container>
</template>

<script>
import { mapGetters, mapState } from "vuex";
export default {
    computed: {
        ...mapGetters(["cartProducts", "cartTotalPrice"]),
        ...mapState(["checkoutStatus"])
    },
    methods: {
        checkout(products) {
            this.$store.dispatch("checkout", products);
        }
    }
};
</script>