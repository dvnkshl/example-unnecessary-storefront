<template>

  <div class="grid grid-cols-3 gap-1 border-gray-700 border-b py-4 px-2">
    <div class="col-span-2">
      <span class="block text-gray-100">{{item.name}} <b>× {{ item.quantity }}</b></span>
    </div>
    <div class="col-span-1 text-right text-green-400">{{item.line_total.formatted_with_symbol}}<br><button class="text-red-300 text-xs" @click="$emit('remove-from-cart', item.id)">Remove</button></div>
  </div>
</template>

<script>
export default {
  name: 'CartItem',
  props: ['item'],
  data() {
    return {
      cartVisible: false,
    };
  },
};
</script>

<style lang="scss">
  .cart-item{
    max-width: 200px;
    img{
      max-width: 100%;
    }
  }
</style>
