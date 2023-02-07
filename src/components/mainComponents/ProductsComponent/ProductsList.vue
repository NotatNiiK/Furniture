<template>
    <ul class="products__list">
        <ProductItem v-for="(item, index) in items" :key="index" :item="item" :index="index" @addtocart="addToCart"
            @addtofavorites="addToFavorites" />
    </ul>
    <div class="products__empty" v-show="items.length == 0">
        <p>Opps... not found!</p>
    </div>
</template>

<script>
import ProductItem from './ProductItem.vue';
export default {
    components: {
        ProductItem,
    },
    props: {
        items: {
            type: Array,
        }
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