<template>
    <div class="cart" v-show="isVisible">
        <div class="cart__wrp">
            <button class="cart__close-btn" @click="closeCartBlock"></button>
            <div class="cart__body" :class="{ 'cart-active': active }">
                <div class="cart__empty-img" v-show="cartArr.length === 0">
                    <img src="../assets/img/Cart/empty-cart.png" alt="Empty">
                </div>
                <template v-for="(item, index) in cartArr" :key="index">
                    <CartItem :item="item" :index="index" @removeitem="removeItem" />
                </template>
            </div>
        </div>
    </div>
</template>

<script>
import CartItem from './cartComponents/CartItem';
export default {
    components: {
        CartItem,
    },
    props: {
        isVisible: {
            type: Boolean
        },
        cartArr: {
            type: Array,
        }
    },
    watch: {
        isVisible(newValue) {
            let vm = this;
            if (newValue) {
                setTimeout(function () {
                    vm.active = true;
                }, 10)
            }
            else {
                vm.active = false;
            }
        }
    },
    data() {
        return {
            active: false,
        }
    },
    methods: {
        closeCartBlock() {
            this.$emit('closecart');
        },
        removeItem(index) {
            this.$emit('remove', index);
        }
    }
}
</script>