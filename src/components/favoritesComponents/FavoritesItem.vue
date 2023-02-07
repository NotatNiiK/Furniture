<template>
    <div class="favorites__column">
        <div class="favorites__item">
            <div class="favorites__img">
                <img :src="item.img" alt="Image">
            </div>
            <div class="favorites__desc">
                <div class="favorites__name">{{ item.name }}</div>
                <div class="favorites__price">{{ item.price }}</div>
            </div>
            <div class="favorites__buttons">
                <button class="favorites__btn" @click="addToCartFromFavorites" :disabled="item.isAdded">{{
                    btnText
                }}</button>
                <button class="favorites__btn" @click="removeItem">Remove</button>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        item: {
            type: Object,
        },
        index: {
            type: Number,
        },
        cartArr: {
            type: Array,
        },
    },
    data() {
        return {
        }
    },
    methods: {
        removeItem() {
            this.$emit('remove', this.index)
        },
        addToCartFromFavorites() {
            this.$emit('addtocartfromfavorites', this.item);
        },
    },
    computed: {
        btnText() {
            return (this.item.isAdded) ? 'Added to cart' : 'Add to cart';
        }
    }
}
</script>
