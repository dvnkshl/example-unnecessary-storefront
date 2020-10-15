<template>

  <div class="cart max-w-sm w-full fixed top-0 right-0 z-10 pt-5 pr-10">

    <div class="grid grid-cols-8 gap-3 justify-items-center content-center   items-center ">

<div v-tilt class="col-span-4 bg-gray-800 shadow-lg rounded-full text-white px-4 py-2 cursor-pointer" @click="cartVisible = !cartVisible">
      <span v-if="!cartVisible">
        Cart
      </span>
      <span v-else>
        Close Cart
      </span>
      <span v-if="cart !== null">(<b>{{this.cart.total_items}}</b>)</span>
    </div>

      <div v-if="cartVisible" class="col-span-8 rounded-md bg-gray-800 shadow-lg w-full px-4" style="transform-style: preserve-3d" v-tilt>
          <div v-if="cart.line_items.length" class="grid-col-3 pt-2">
            <CartItem
            @remove-from-cart="$emit('remove-from-cart', $event)"
            v-for="(item, index) in cart.line_items"
            :key="index"
            :item="item"
          />
         </div>
         <div v-else class="grid-col-3">
           <p class="text-center text-gray-500 pt-6">Your cart appears to be empty</p>
         </div>
         <div class="grid grid-cols-4 gap-1 text-lg p-2 py-4" style="transform: translateZ(20px)">

            <div class="col-span-3" >
             <b class="block text-gray-100 py-1">Subtotal</b>
            </div>

            <div class="col-span-1 text-right text-green-500 py-1">
              <b>{{cart.subtotal.formatted_with_symbol}}</b>
            </div>

            <div class="col-span-2 py-3" >
             <button class="hover:bg-red-900 text-white text-xs py-1 px-2 border hover:border-red-900 border-gray-400 rounded shadow" @click="$emit('clear-cart')" style="transform: translateZ(20px)">Clear Cart</button>
            </div>
            <div class="col-span-2 text-right text-green-500 py-2">
              <button v-if="cart.line_items.length > 0" class="hover:bg-green-800 hover:border-green-800  text-white text-md py-2 px-3 border bg-green-600 border-green-600 rounded shadow" @click="$emit('checkout')" style="transform: translateZ(20px)">Checkout</button>
            </div>

      </div>

    </div>

</div>
  </div>
</template>

<script>
import CartItem from './CartItem.vue';

export default {
  name: 'Cart',
  props: ['cart'],
  components: {
    CartItem,
  },
  data() {
    return {
      cartVisible: false,
    };
  },
};
</script>
<!--<div class="w-3/12 rounded-md bg-gray-800 shadow-lg m-32 antialiased">
  <div class="grid grid-cols-3 gap-1 border-gray-700 border-b p-4">
    <div class="col-span-2">
      <span class="block text-white">Product Name</span>
      <span class="text-sm text-white opacity-75 font-light">Product Price</span>
    </div>
    <div class="col-span-1 text-right text-green-400">$230</div>
  </div>

</div>!-->
<style lang="scss">


</style>
