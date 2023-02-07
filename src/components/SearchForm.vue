<template>
    <div class="search-form">
        <input type="text" class="search-form__input" v-model="value" @input="searchItem">
        <button class="search-form__button" @click="closeForm">&times;</button>
    </div>
</template>

<script>
export default {
    props: {
        searchValue: String,
    },
    data() {
        return {
            value: this.searchValue,
        }
    },
    methods: {
        searchItem() {
            this.$emit('searchItem', this.value);
        },
        closeForm() {
            this.value = '';
            this.$emit('closeForm');
        }
    }
}
</script>