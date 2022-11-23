<template>
  <component :is="CurrentPageComponent" :page-params="currentPageParams" @gotoPage="(pageName, pageParams) => gotoPage(pageName, pageParams)"></component>
</template>

<script>
import MainPage from './pages/MainPage.vue';
import ProductPage from './pages/ProductPage.vue';
import NotPage from './pages/NotPage.vue';

const routes = {
  'main': MainPage,
  'product': ProductPage,
}

export default {
  name: 'App',
  data() {
    return {
      currentPage: 'main',
      currentPageParams: {},
    }
  },
  components: {
    MainPage,
    ProductPage,
    NotPage,
  },
  computed: {
    CurrentPageComponent() {
      return routes[this.currentPage] || NotPage;
    }
  },
  methods: {
    gotoPage(pageName, pageParams) {
      this.currentPage = pageName;
      this.currentPageParams = pageParams || {};
    }
  }
}
</script>

<style>
</style>
