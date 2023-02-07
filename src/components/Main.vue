<template>
    <main class="main">
        <Intro />
        <Products :products-arr="itemsArr" @refresh="refreshItem" @addtocart="addToCart"
            @addtofavorites="addToFavorites">Best Seller Items</Products>
        <Deal />
        <Trending @tabs-filter="tabsFilter" />
        <Products :products-arr="trendingArr" @addtocart="addToCart" @addtofavorites="addToFavorites"
            class="nonePadding" />
        <Contacts />
    </main>
</template>

<script>
import Intro from './mainComponents/Intro.vue';
import Products from './mainComponents/Products.vue';
import Deal from './mainComponents/Deal.vue';
import Trending from './mainComponents/Trending.vue';
import Contacts from './mainComponents/Contacts.vue';
export default {
    components: {
        Intro,
        Products,
        Deal,
        Trending,
        Contacts,
    },
    props: {
        itemsArr: {
            type: Array,
        },
        trendingArr: Array,
    },
    methods: {
        addToCart(item) {
            this.$emit('addtocart', item);
        },
        addToFavorites(item) {
            this.$emit('addtofavorites', item);
        },
        tabsFilter(value) {
            this.$emit('tabsFilter', value)
        },
    }
}
</script>