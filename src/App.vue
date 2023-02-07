<template>
  <div class="wrapper" ref="wrapper">
    <Header :cartitems="cartItems" :favoritesitems="favoritesitems" @opencart="openCartBlock" @showForm="showSearchForm"
      :style="{ 'padding-right': paddingRight }" :class="{ 'scrolled': isScrolled }"
      @openfavorites="openFavoritesBlock" />
    <Main :items-arr="filteredArr" :trending-arr="sortedTabsArr" @addtocart="addToCart" @addtofavorites="addToFavorites"
      @tabs-filter="tabsFilter" />
    <Cart :is-visible="isCartBlockVisible" @closecart="closeCartBlock" :cart-arr="cartItemsArr"
      @remove="removeFromCart" />
    <Favorites :is-visible="isFavoritesBlockVisible" :favorites-arr="favoritesArr" :cart-arr="cartItemsArr"
      @closefavorites="closeFavoritesBlock" @removeitem="removeFromFavorites" @addtocartfromfavorites="addToCart" />
    <SearchForm :class="{ 'search-form-active': isSearchFormActive }" :search-value="searchFormValue"
      @search-item="searchItem" @close-form="closeForm" />
    <Footer />
  </div>
</template>

<script>
import Header from './components/Header.vue';
import Main from './components/Main.vue';
import Footer from './components/Footer.vue';
import Cart from './components/Cart.vue';
import Favorites from './components/Favorites.vue';
import SearchForm from './components/SearchForm.vue';

export default {
  components: {
    Header,
    Main,
    Footer,
    Cart,
    Favorites,
    SearchForm,
  },
  data() {
    return {
      isCartBlockVisible: false,
      isFavoritesBlockVisible: false,
      paddingRight: '0px',
      isSearchFormActive: false,
      searchFormValue: '',
      cartItems: 0,
      favoritesitems: 0,
      isScrolled: false,
      productsItem: [
        { img: 'img/01.png', name: "Metal Vintage Pendant", price: "$79", hot: true, discount: '-5%', isAdded: false, },
        { img: 'img/02.png', name: "Klosh Table Clock", price: "$99", hot: false, discount: '', isAdded: false, },
        { img: 'img/03.png', name: "Arne Dining Chair", price: "$350", hot: false, discount: '', isAdded: false, },
        { img: 'img/04.png', name: "Klosh Wall Clock", price: "$129", hot: true, discount: '', isAdded: false, },
        { img: 'img/05.png', name: "Modern Outdoor Chair", price: "$79", hot: true, discount: '-20%', isAdded: false, },
        { img: 'img/06.png', name: "Vipp Wool Pillow", price: "$99", hot: false, discount: '', isAdded: false, },
        { img: 'img/07.png', name: "Modern Bedroom Storage", price: "$499", hot: true, discount: '-17%', isAdded: false, },
      ],
      randomNums: [],
      cartItemsArr: [],
      favoritesArr: [],
      trendingArr1: [
        { img: 'img/Trending/01.png', name: "Metal Vintage Pendant", price: "$79", hot: true, discount: '-5%', isAdded: false, },
        { img: 'img/Trending/02.png', name: "Klosh Table Clock", price: "$99", hot: false, discount: '', isAdded: false, },
        { img: 'img/Trending/03.png', name: "Arne Dining Chair", price: "$350", hot: false, discount: '', isAdded: false, },
        { img: 'img/Trending/04.png', name: "Klosh Wall Clock", price: "$129", hot: true, discount: '', isAdded: false, },
      ],
      trendingArr2: [
        { img: 'img/Trending/02.png', name: "Metal Vintage Pendant", price: "$79", hot: true, discount: '-5%', isAdded: false, },
        { img: 'img/Trending/03.png', name: "Klosh Table Clock", price: "$99", hot: false, discount: '', isAdded: false, },
      ],
      trendingArr3: [
        { img: 'img/Trending/01.png', name: "Metal Vintage Pendant", price: "$79", hot: true, discount: '-5%', isAdded: false, },
        { img: 'img/Trending/04.png', name: "Klosh Wall Clock", price: "$129", hot: true, discount: '', isAdded: false, },
      ],
      trendingArr4: [
        { img: 'img/Trending/04.png', name: "Metal Vintage Pendant", price: "$79", hot: true, discount: '-5%', isAdded: false, },
        { img: 'img/Trending/03.png', name: "Klosh Table Clock", price: "$99", hot: false, discount: '', isAdded: false, },
        { img: 'img/Trending/02.png', name: "Arne Dining Chair", price: "$350", hot: false, discount: '', isAdded: false, },
        { img: 'img/Trending/01.png', name: "Klosh Wall Clock", price: "$129", hot: true, discount: '', isAdded: false, },
      ],
      trendingArr5: [
        { img: 'img/Trending/03.png', name: "Klosh Table Clock", price: "$99", hot: false, discount: '', isAdded: false, },
        { img: 'img/Trending/01.png', name: "Klosh Wall Clock", price: "$129", hot: true, discount: '', isAdded: false, },
      ],
      trendingArr6: [
        { img: 'img/Trending/04.png', name: "Metal Vintage Pendant", price: "$79", hot: true, discount: '-5%', isAdded: false, },
      ],
      tabsFilterValue: '',
    }
  },
  created() {
    window.addEventListener('scroll', this.handleScroll);
  },
  destroyed() {
    window.removeEventListener('scroll', this.handleScroll);
  },
  methods: {
    handleScroll() {
      if (pageYOffset > 60) {
        this.isScrolled = true;
      } else {
        this.isScrolled = false;
      }
    },
    openCartBlock() {
      let scrollWidth = window.innerWidth - this.$refs.wrapper.offsetWidth + 'px';
      document.body.style.paddingRight = scrollWidth;
      this.paddingRight = scrollWidth;
      document.body.classList.add('lock');
      document.documentElement.addEventListener('keyup', (event) => {
        if (event.code === 'Escape')
          this.isCartBlockVisible = false;
        document.body.classList.remove('lock');
        document.body.style.paddingRight = '0px';
        this.paddingRight = '0px';
      });
      this.isCartBlockVisible = true;
    },
    closeCartBlock() {
      document.body.classList.remove('lock');
      document.body.style.paddingRight = '0px';
      this.paddingRight = '0px';
      this.isCartBlockVisible = false;
    },
    openFavoritesBlock() {
      let scrollWidth = window.innerWidth - this.$refs.wrapper.offsetWidth + 'px';
      document.body.style.paddingRight = scrollWidth;
      this.paddingRight = scrollWidth;
      document.body.classList.add('lock');
      document.documentElement.addEventListener('keyup', (event) => {
        if (event.code === 'Escape')
          this.isFavoritesBlockVisible = false;
        document.body.classList.remove('lock');
        document.body.style.paddingRight = '0px';
        this.paddingRight = '0px';
      });
      this.isFavoritesBlockVisible = true;
    },
    searchItem(value) {
      this.searchFormValue = value;
    },
    closeForm() {
      this.searchFormValue = '';
      this.isSearchFormActive = false;
    },
    closeFavoritesBlock() {
      document.body.classList.remove('lock');
      document.body.style.paddingRight = '0px';
      this.paddingRight = '0px';
      this.isFavoritesBlockVisible = false;
    },
    addToCart(item) {
      if (!this.cartItemsArr.includes(item)) {
        item.isAdded = true;
        this.cartItemsArr.push(item);
        this.cartItems++;
      }
    },
    addToFavorites(item) {
      if (!this.favoritesArr.includes(item)) {
        this.favoritesArr.push(item);
        this.favoritesitems++;
      }
    },
    removeFromFavorites(index) {
      this.favoritesArr.splice(index, 1);
      this.favoritesitems--;
    },
    removeFromCart(index) {
      this.cartItemsArr[index].isAdded = false;
      this.cartItemsArr.splice(index, 1);
      this.cartItems--;
    },
    getRndInteger(min, max) {
      if (this.randomNums.length == 7) {
        this.randomNums.length = 0;
      }
      let num = Math.floor(Math.random() * (max - min + 1)) + min;
      if (!this.randomNums.includes(num)) {
        this.randomNums.push(num);
        console.log(num)
        return num;
      } else {
        this.getRndInteger(min, max)
      }
    },
    tabsFilter(value) {
      this.tabsFilterValue = value;
    },
    showSearchForm() {
      this.isSearchFormActive = !this.isSearchFormActive
    },
  },
  computed: {
    filteredArr() {
      let productName = this.searchFormValue.toLowerCase();
      if (productName) {
        let arrFiltered = this.productsItem.filter(item => item.name.toLowerCase().indexOf(productName) > -1);
        return arrFiltered;
      }
      else {
        return this.productsItem;
      }
    },
    sortedTabsArr() {
      switch (this.tabsFilterValue) {
        case 'table':
          return this.trendingArr1;
          break;
        case 'lamp':
          return this.trendingArr2;
          break;
        case 'cabinet':
          return this.trendingArr3;
          break;
        case 'sofa':
          return this.trendingArr4;
          break;
        case 'chair':
          return this.trendingArr5;
          break;
        case 'bed':
          return this.trendingArr6;
          break;
        default:
          return this.trendingArr1;
          break;
      }
    }
  }
}
</script>

<style>

</style>
