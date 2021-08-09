<template>
    <v-container>
        <v-layout justify-center>
            <ul class="pt-10 list-style-type:none">
                <v-list v-for="product in products" :key="product.id" class="pt-10">
                    <v-card class="px-4">{{product.title}} - {{product.price}}</v-card>
                    <br />
                    <v-btn
                        rounded
                        @click="addProductToCart(product)"
                        :disabled="!product.inventory"
                    >Add to cart</v-btn>
                </v-list>
            </ul>
        </v-layout>
    </v-container>
</template>

<script>
import { mapState } from "vuex";
export default {
    computed: mapState(["products"]),
    methods: {
        addProductToCart: function(product) {
            this.$store.dispatch("addProductToCart", product);
        }
    },
    created: function() {
        this.$store.dispatch("getAllProducts");
    }
};
</script>