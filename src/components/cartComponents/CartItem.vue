<template>
    <div class="cart__item item-cart">
        <div class="item-cart__img">
            <img :src="item.img" alt="Item">
        </div>
        <div class="item-cart__description">
            <div class="item-cart__info">
                <div class="item-cart__name">{{ item.name }}</div>
                <div class="item-cart__price">{{ finalPrice }}</div>
                <div class="item-cart__num-of-items num-of-items">
                    <button class="num-of-items__btn" @click="decreaseNumberOfItems">
                        <span>-</span>
                    </button>
                    <input type="number" class="num-of-items__input" v-model="numberOfItems">
                    <button class="num-of-items__btn" @click="increaseNumberOfItems">
                        <span>+</span>
                    </button>
                </div>
            </div>
            <div class="item-cart__buttons">
                <button class="item-cart__btn">Buy</button>
                <button class="item-cart__btn" @click="removeItem">Remove</button>
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
            type: Number
        }
    },
    data() {
        return {
            numberOfItems: 1,
        }
    },
    methods: {
        decreaseNumberOfItems() {
            if (this.numberOfItems > 0) {
                this.numberOfItems--;
            }
        },

        increaseNumberOfItems() {
            this.numberOfItems++;
        },
        removeItem() {
            this.$emit('removeitem', this.index);
        }
    },
    computed: {
        finalPrice() {
            if (this.numberOfItems === 1) {
                return this.item.price;
            }
            else {
                let price = '$' + this.item.price.slice(1) * this.numberOfItems;
                return price;
            }
        }
    }
}
</script>

<style>

</style>