<template>
    <header class="header _anim-items">
        <div class="header__container">
            <div class="header__body">
                <div class="header__logo">
                    <a href="#" class="_icon-logo"></a>
                </div>
                <nav class="header__nav" :class="{ 'activeNav': isNavActive }">
                    <ul class="header__list">
                        <li class="header__item">
                            <a href="#" class="header__link">Home</a>
                        </li>
                        <li class="header__item">
                            <a href="#" class="header__link">Shop</a>
                        </li>
                        <li class="header__item">
                            <a href="#" class="header__link">Product</a>
                        </li>
                        <li class="header__item">
                            <a href="#" class="header__link">Blog</a>
                        </li>
                        <li class="header__item">
                            <a href="#" class="header__link">Page</a>
                        </li>
                        <li class="header__item">
                            <a href="#" class="header__link">Contact</a>
                        </li>
                    </ul>
                </nav>
                <div class="header__buttons">
                    <button class="header__button _icon-search" @click="openSearchForm"></button>
                    <button class="header__button _icon-cart" @click="openCartBlock">
                        <p v-show="cartitems > 0">
                            <span>{{ cartitems }}</span>
                        </p>
                    </button>
                    <button class="header__button _icon-like" @click="openFavoritesBlock">
                        <p v-show="favoritesitems > 0" class="red">
                            <span>{{ favoritesitems }}</span>
                        </p>
                    </button>
                </div>
                <div class="header__burger" :class="{ activeBurger: isBurgerActive }" @click="showBurgerMenu">
                    <span></span>
                </div>
            </div>
        </div>
    </header>
</template>

<script>
export default {
    props: {
        cartitems: {
            type: Number,
        },
        favoritesitems: {
            type: Number
        }
    },
    data() {
        return {
            isNavActive: false,
            isBurgerActive: false,
            activeInput: false,
        }
    },
    methods: {
        showBurgerMenu() {
            this.isNavActive = !this.isNavActive;
            this.isBurgerActive = !this.isBurgerActive;
        },
        openCartBlock() {
            this.$emit('opencart');
        },
        openFavoritesBlock() {
            this.$emit('openfavorites');
        },
        openSearchForm() {
            this.$emit('showForm');
        }
    }
}
</script>