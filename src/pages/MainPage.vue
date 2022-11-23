<template>
    <main class="content container">
    <div class="content__top content__top--catalog">
      <h1 class="content__title">
        Каталог
      </h1>
      <span class="content__info">
        152 товара
      </span>
    </div>

    <div class="content__catalog">
      <ProductFilter v-model:priceFrom="this.filterPriceFrom" v-model:priceTo="this.filterPriceTo" v-model:categoryId="this.filterCategoryId"/>
      <section class="catalog">
        <ProductList :products="products" @gotoPage="(pageName, pageParams) => $emit('gotoPage', pageName, pageParams)"></ProductList>
        <BasePagination :page="page" @paginate="this.page = $event" :count="countProducts" :per-page="productsPerPage"></BasePagination>
      </section>
    </div>
  </main>
</template>

<script>
import products from './../data/products';
import ProductList from './../components/ProductList.vue';
import ProductFilter from './../components/ProductFilter.vue';
import BasePagination from './../components/BasePagination.vue';

export default {
  name: 'MainPage',
  components: {
    ProductList,
    ProductFilter,
    BasePagination,
  },
  data() {
    return {
      page: 1,
      productsPerPage: 3,

      filterPriceFrom: 0,
      filterPriceTo: 0,
      filterCategoryId: 0,
    }
  },
  computed: {
    filteredProducts() {
      let filteredProducts = products;

      if (this.filterPriceFrom > 0) {
        filteredProducts = filteredProducts.filter(product => product.price >= this.filterPriceFrom);
      }

      if (this.filterPriceTo > 0) {
        filteredProducts = filteredProducts.filter(product => product.price <= this.filterPriceTo);
      }

      if (this.filterCategoryId > 0) {
        filteredProducts = filteredProducts.filter(product => product.categoryId === this.filterCategoryId);
      }

      return filteredProducts;
    },
    products() {
      const offset = (this.page - 1) * this.productsPerPage;
      return this.filteredProducts.slice(offset, offset + this.productsPerPage);
    },
    countProducts() {
      return this.filteredProducts.length;
    }
  }
}

</script>