<template>
    <div class="favorites" v-show="isVisible">
        <div class="favorites__wrp">
            <button class="favorites__close-btn" @click="closeFavorites"></button>
            <div class="favorites__body" :class="{ 'favorites-active': active }">
                <div class="favorites__empty-img" v-show="favoritesArr.length === 0">
                    <img src="../assets/img/Favorites/Empty.webp" alt="Empty">
                </div>
                <div class="favorites__row">
                    <template v-for="(item, index) in favoritesArr" :key="index">
                        <FavoritesItem :item="item" :index="index" @remove="removeItem"
                            @addtocartfromfavorites="addToCartFromFavorites" :cart-arr="cartArr" />
                    </template>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import FavoritesItem from './favoritesComponents/FavoritesItem.vue';
export default {
    components: {
        FavoritesItem,
    },
    props: {
        isVisible: {
            type: Boolean,
        },
        favoritesArr: {
            type: Array,
        },
        cartArr: {
            type: Array,
        },
    },
    data() {
        return {
            active: false,
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
    methods: {
        closeFavorites() {
            this.$emit('closefavorites')
        },
        removeItem(index) {
            this.$emit('removeitem', index)
        },
        addToCartFromFavorites(item) {
            this.$emit('addtocartfromfavorites', item)
        }
    }
}
</script>
