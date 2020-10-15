<template>
  <div>
    <h2 class="text-3xl font-light text-gray-800 text-center py-20  ">
        Commerce.js Unnecessary Parallax Storefront
    </h2>
    <div v-if="this.filteredItems"
      class="product-listing grid grid-cols-3 gap-6"
    >
        <ProductItem
          @add-to-cart="$emit('add-to-cart', $event)"
          v-for="(product, index) in filteredItems" :key="index"
          :product="product"
          :index="index"
        />
    </div>

  </div>
</template>

<script>
import ProductItem from './ProductItem.vue';

export default {
  name: 'ProductLanding',
  props: {
    products: {
      type: Array,
      default: () => [],
    },
    merchant: {
      type: Object,
      default: () => [],
    },
  },
  data() {
    return {
      selectedCategory: '',
      categories: [],
    };
  },
  components: {
    ProductItem,
  },
  mounted() {
    this.getCategories();
  },
  computed: {
    /**
     * Filters the visible products based on the category
     * selected. If no category is selected, it returns
     * all products.
     */
    filteredItems() {
      let filteredProducts = this.products;

      if (this.selectedCategory !== '') {
        filteredProducts = this.products.filter((product) => product.categories.length > 0
          && product.categories[0].name === this.selectedCategory);
      }

      return filteredProducts;
    },
  },
  methods: {
    /**
     * Retrieve a list of the categories.
     * https://commercejs.com/docs/sdk/products#list-categories
     *
     * @return {object} List of categories.
     */
    getCategories() {
      this.$commerce.categories.list().then((result) => {
        this.categories = result;
      }).catch((error) => {
        console.error(`Category Retreval Error: ${error.message}`);
      });
    },
  },
};
</script>

<style lang="scss">
  .product-listing{
    @apply flex-grow p-4 grid grid-cols-3 gap-1 mx-auto;

  }

</style>
