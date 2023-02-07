<template>
    <div class="trending">
        <div class="trending__container">
            <h2 class="trending__title">TRENDING CATEGORIES</h2>
            <div class="trending__tabs">
                <div class="trending__tab" @click="tabsFilter('table')" :class="{'active-tab':activeTab1}">
                    <div class="trending__tab-content tab">
                        <img src="../../assets/img/Main/Trending/01.svg" alt="Icon">
                        <p class="tab__name">DRESSING TABLE</p>
                    </div>
                </div>
                <div class="trending__tab" @click="tabsFilter('lamp')" :class="{ 'active-tab': activeTab2 }">
                    <div class="trending__tab-content tab">
                        <img src="../../assets/img/Main/Trending/02.svg" alt="Icon">
                        <p class="tab__name">LAMP</p>
                    </div>
                </div>
                <div class="trending__tab" @click="tabsFilter('cabinet')" :class="{ 'active-tab': activeTab3 }">
                    <div class="trending__tab-content tab">
                        <img src="../../assets/img/Main/Trending/03.svg" alt="Icon">
                        <p class="tab__name">CABINET</p>
                    </div>
                </div>
                <div class="trending__tab" @click="tabsFilter('sofa')" :class="{ 'active-tab': activeTab4 }">
                    <div class="trending__tab-content tab">
                        <img src="../../assets/img/Main/Trending/04.svg" alt="Icon">
                        <p class="tab__name">SOFA</p>
                    </div>
                </div>
                <div class="trending__tab" @click="tabsFilter('chair')" :class="{ 'active-tab': activeTab5 }">
                    <div class="trending__tab-content tab">
                        <img src="../../assets/img/Main/Trending/05.svg" alt="Icon">
                        <p class="tab__name">CHAIR</p>
                    </div>
                </div>
                <div class="trending__tab" @click="tabsFilter('bed')" :class="{ 'active-tab': activeTab6 }">
                    <div class="trending__tab-content tab">
                        <img src="../../assets/img/Main/Trending/06.svg" alt="Icon">
                        <p class="tab__name">BED</p>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            activeTab1: true,
            activeTab2: false,
            activeTab3: false,
            activeTab4: false,
            activeTab5: false,
            activeTab6: false,
        }
    },
    methods: {
        tabsFilter(value, event) {
            if (value === 'table') {
                this.activeTab1 = true;
                this.activeTab2 = false;
                this.activeTab3 = false;
                this.activeTab4 = false;
                this.activeTab5 = false;
                this.activeTab6 = false;
            }
            else if (value === 'lamp') {
                this.activeTab1 = false;
                this.activeTab2 = true;
                this.activeTab3 = false;
                this.activeTab4 = false;
                this.activeTab5 = false;
                this.activeTab6 = false;
            }
            else if (value === 'cabinet') {
                this.activeTab1 = false;
                this.activeTab2 = false;
                this.activeTab3 = true;
                this.activeTab4 = false;
                this.activeTab5 = false;
                this.activeTab6 = false;
            }
            else if (value === 'sofa') {
                this.activeTab1 = false;
                this.activeTab2 = false;
                this.activeTab3 = false;
                this.activeTab4 = true;
                this.activeTab5 = false;
                this.activeTab6 = false;
            }
            else if (value === 'chair') {
                this.activeTab1 = false;
                this.activeTab2 = false;
                this.activeTab3 = false;
                this.activeTab4 = false;
                this.activeTab5 = true;
                this.activeTab6 = false;
            }
            else if (value === 'bed') {
                this.activeTab1 = false;
                this.activeTab2 = false;
                this.activeTab3 = false;
                this.activeTab4 = false;
                this.activeTab5 = false;
                this.activeTab6 = true;
            }
            this.$emit('tabsFilter', value)
        }
    }
}
</script>