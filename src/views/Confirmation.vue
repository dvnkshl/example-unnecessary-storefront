<template>
  <div>
    <canvas id="confetti" class="fixed z-0 left-0 t-0"></canvas>
  <div class="text-center p-32 relative z-1">
    <p class="text-gray-700 text-6xl pb-6">🎉</p>
            <p class="text-gray-700 text-3xl pb-6"> Your order has been received!</p>
            <p class="text-gray-700 text-xl pb-6"><strong>Order Reference:</strong> #{{orderRef}}</p>
            <p class="font-light text-xl text-gray-800 py-5 text-center ">View the <a class="text-blue-600 underline" href="https://github.com/dvnkshl/example-unnecessary-storefront">code on GitHub</a></p>

</div>
  </div>
</template>

<script>
import ConfettiGenerator from "confetti-js";
export default {
  name: 'Confirmation',
  props: ['orderRef', 'merchant'],
  mounted() {
          var confetti = new ConfettiGenerator({ target: 'confetti', max: 1000, size: 1, clock :"50", start_from_edge :false, respawn:false});
          confetti.render();
        return;
    },
};
</script>
