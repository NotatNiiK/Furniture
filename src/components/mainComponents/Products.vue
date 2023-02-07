<template>
    <div class="products">
        <div class="products__container">
            <h2 class="products__title">
                <slot></slot>
            </h2>
            <ProductsList :items="productsArr" @addtocart="addToCart" @addtofavorites="addToFavorites" />
        </div>
    </div>
</template>

<script>
import ProductsList from './ProductsComponent/ProductsList.vue';
export default {
    components: {
        ProductsList,
    },
    props: {
        productsArr: {
            type: Array,
        },
    },
    methods: {
        addToCart(item) {
            this.$emit('addtocart', item);
        },
        addToFavorites(item) {
            this.$emit('addtofavorites', item);
        }
    }
}
</script>