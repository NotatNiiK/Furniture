<template>
    <li class="products__item item">
        <div class="item__body">
            <div class="item__add-info">
                <div class="item__bonus" v-show="item.hot">HOT</div>
                <div class="item__bonus" v-show="item.discount">{{ item.discount }}</div>
            </div>
            <div class="item__panel">
                <button class="item__btn _icon-heart" @click="addToFavorites"></button>
                <button class="item__btn _icon-Cart" @click="addToCart"></button>
            </div>
            <div class="item__img">
                <img :src='item.img' alt="asd">
            </div>
            <div class="item__description">
                <div class="item__name">{{ item.name }}</div>
                <div class="item__price">{{ item.price }}</div>
            </div>
        </div>
    </li>
</template>

<script>
export default {
    props: {
        item: {
            type: Object,
        },
        index: {
            type: Number,
        }
    },
    methods: {
        addToCart() {
            this.$emit('addtocart', this.item);
        },
        addToFavorites() {
            this.$emit('addtofavorites', this.item);
        }
    }
}
</script>