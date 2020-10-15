<template>
    <div class="product-item m-4" v-if="product">
    <div v-tilt="{scale: 1.05, speed: 500, perspective: 1200}" class="overflow-hidden rounded-md mx-5
    my-2 relative shadow-sm hover:shadow-xl w-auto">
      <div class="transition duration-200 ease-in-out w-full h-full absolute
                  opacity-0 hover:opacity-100 bg-black bg-opacity-50 z-10 flex">
        <div class="m-auto w-64">
          <a
          @click="addToCart()"
          :disabled="quantityWarning.enabled"
          class="transition duration-200 ease-in-out bg-white block text-center my-4 py-4
                    rounded-sm shadow-lg hover:bg-green-600 hover:text-white cursor-pointer">Add to Cart</a>
        </div>
      </div>
      <div >
        <img :src="product.media.source" onerror="this.style.display='none';" class="w-100 h-100
        shadow-sm" />
      </div>
    </div>
    <div class="grid grid grid-cols-6 mx-5 ">
      <span class="col-span-4">{{product.name}}</span>
      <span class="col-span-2 text-right text-green-600">
        {{product.price.formatted_with_symbol}}
        </span>
    </div>
    </div>
</template>

<script>
export default {
  name: 'ProductItem',
  props: ['product', 'index'],
  data() {
    return {
      selectedVariant: '',
      selectedAmount: 1,
      quantityWarning: {
        enabled: false,
        amount: '',
      },
    };
  },
  methods: {
    /**
     * Checks the instock quantity for the product
     * and disables the add to cart button if
     * not enough stock is available.
     */
    checkQuantity() {
      this.quantityWarning.enabled = false;
      let amount = this.product.quantity;
      if (this.product.variants) {
        amount = this.selectedVariant.quantity;
      }
      if (amount < this.selectedAmount) {
        this.quantityWarning.enabled = true;
        this.quantityWarning.amount = amount;
      }
    },
    /**
     * Add the product to the cart.
     */
    addToCart() {
      let variant = null;
      if (this.product.variants.length !== 0) {
        variant = { [this.product.variants[0].id]: this.selectedVariant.id };
      }
      this.$emit('add-to-cart', {
        productId: this.product.id,
        productAmount: this.selectedAmount,
        productVariant: variant,
      });
    },
  },
};
</script>

<style lang="scss">
  .product-item{
  }
</style>
