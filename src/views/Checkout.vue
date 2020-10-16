<template>
    <section>
        <canvas id="confetti" class="fixed z-0 left-0 t-0"></canvas>
        <div v-if="liveObject !== null" class="place-items-stretch grid">

            <h2 class="text-3xl font-light text-gray-800 text-center py-20  ">
                Commerce.js's Unnecessary Parallax Storefront
            </h2>

            <a href="/" class="text-sm cursor-pointer absolute top-0 right-0 bg-gray-800 text-center  text-white rounded mt-10 mr-10 px-4 rounded-full py-2  shadow-lg" style="transform: translateZ(20px)"><b>Go back</b> to the storefront</a>

             <div v-if="message.copy !== ''" v-tilt class="bg-red-600 px-4 py-3 text-white block place-self-center place-self-center rounded-md shadow-md fixed left-0 top-0 mt-5 ml-5">
                <strong>Error!</strong> an error occured:
                <p v-html="message.copy">Loading...</p>
            </div>


            <div class="w-74 px-10 max-w-4xl place-self-center" v-tilt="{scale: 1.0, speed: 500, perspective: 3000}">

                <div v-if="isCapturing" class="col-span-8 rounded-md bg-gray-800 shadow-lg p-20 text-center" style="transform-style: preserve-3d" v-tilt>
                    <p class="text-white text-3xl pb-6"> 🎉 Placing order 💫</p>
                    <div class="loader ease-linear rounded-full border-4 border-t-4 border-gray-700 h-32 w-32 m-auto" style="transform: translateZ(20px);"></div>
                    <p class="text-white pt-6"> Enjoy the unnecessary<br>✨ c ✨ o ✨ n ✨ f ✨ e ✨ t ✨ t ✨ i ✨ </p>
                </div>

                <div v-else>
                    <div class="grid grid-cols-8 gap-4 content-center px-40 py-5 items-center">

                        <div class="col-span-8">
                            <p class="text-xl text-gray-700" style="transform: translateZ(20px)">Customer</p>
                        </div>
                        <div class="col-span-4">
                            <input v-tilt="{scale: 1.2}" class="input focus:outline-none focus:shadow-outline" type="text" placeholder="First Name" v-model="fields.customer.firstname">
                        </div>
                        <div class="col-span-4">
                            <input v-tilt="{scale: 1.2}" class="input focus:outline-none focus:shadow-outline" type="text" placeholder="Last Name" v-model="fields.customer.lastname">
                        </div>
                        <div class="col-span-8">
                            <input v-tilt="{scale: 1.2}" class="input focus:outline-none focus:shadow-outline" type="text" placeholder="Email Address" v-model="fields.customer.email">
                        </div>
                    </div>

                    <div class="grid grid-cols-8 gap-4 content-center px-40 py-5  items-center">
                        <div class="col-span-8">
                            <p class="text-xl text-gray-700" style="transform: translateZ(20px)">Shipping Address</p>
                        </div>
                        <div class="col-span-8">
                            <input v-tilt="{scale: 1.2}" class="input focus:outline-none focus:shadow-outline" type="text" placeholder="Name" v-model="fields.shipping.name">
                        </div>

                        <div class="col-span-8">
                            <div v-tilt="{scale: 1.2}" class="inline-block relative w-full">
                                <select class="input leading-tight focus:outline-none focus:shadow-outline" v-model="fields.shipping.country" name="">
                                 <option value="">Choose a Shipping Country</option>
                                  <option
                                    :key="index"
                                    v-for="(country, index) in shippingCountries"
                                    :value="index"
                                  >
                                    {{country}}
                                  </option>
                              </select>
                                <div class="pointer-events-none absolute inset-y-0 right-0 flex items-center px-2 text-gray-700">
                                    <svg class="fill-current h-4 w-4" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20"><path d="M9.293 12.95l.707.707L15.657 8l-1.414-1.414L10 10.828 5.757 6.586 4.343 8z"/></svg>
                                </div>
                            </div>

                        </div>

                        <div class="col-span-8">
                            <input v-tilt="{scale: 1.2}" class="input focus:outline-none focus:shadow-outline" type="text" placeholder="Street Address" v-model="fields.shipping.street">
                        </div>

                        <div class="col-span-3">

                            <input v-tilt="{scale: 1.2}" class="input focus:outline-none focus:shadow-outline" type="text" placeholder="City/Town" v-model="fields.shipping.town_city">

                        </div>

                        <div class="col-span-3">
                            <div v-tilt="{scale: 1.2}" class="inline-block relative w-full">
                                <select class="input leading-tight focus:outline-none focus:shadow-outline" v-model="fields.shipping.county_state" name="">
                                 <option value="">Choose a State</option>
                                  <option
                                    :key="index"
                                    v-for="(state, index) in shippingStates"
                                    :value="index.split('-')[1]"
                                  >
                                    {{state}}
                                  </option>
                              </select>
                                <div class="pointer-events-none absolute inset-y-0 right-0 flex items-center px-2 text-gray-700">
                                    <svg class="fill-current h-4 w-4" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20"><path d="M9.293 12.95l.707.707L15.657 8l-1.414-1.414L10 10.828 5.757 6.586 4.343 8z"/></svg>
                                </div>
                            </div>


                        </div>

                        <div class="col-span-2">
                            <input v-tilt="{scale: 1.2}" class="origin-center input focus:outline-none focus:shadow-outline transition-center" type="text" placeholder="Post/Zipcode" v-model="fields.shipping.postal_zip_code">
                        </div>

                    </div>

                    <div class="grid grid-cols-8 gap-4 content-center px-40 py-5  items-center">
                        <div class="col-span-8">
                            <p class="text-xl text-gray-700">Shipping method</p>
                        </div>
                        <div class="col-span-8">

                            <div v-tilt="{scale: 1.2}" class="inline-block relative w-64">
                                <select class="input leading-tight focus:outline-none focus:shadow-outline" v-model="fields.fulfillment.shipping_method" name="">
                                  <option value="">Choose a shipping method</option>
                                  <option
                                    :key="index"
                                    v-for="(option, index) in shippingOptions"
                                    :value="option.id"
                                  >
                                    {{option.description}} - {{option.price.formatted_with_symbol}}
                                  </option>
                                </select>
                                <div class="pointer-events-none absolute inset-y-0 right-0 flex items-center px-2 text-gray-700">
                                    <svg class="fill-current h-4 w-4" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20"><path d="M9.293 12.95l.707.707L15.657 8l-1.414-1.414L10 10.828 5.757 6.586 4.343 8z"/></svg>
                                </div>
                            </div>


                        </div>


                    </div>

                    <div class="grid grid-cols-8 gap-4 content-center px-40 py-5  items-center">
                        <div class="col-span-8">
                            <p class="text-xl text-gray-700">Payment Details</p>
                        </div>
                        <div class="col-span-8">
                            <label>Card Number</label>
                            <input v-tilt="{scale: 1.2}" class="input focus:outline-none focus:shadow-outline" type="text" placeholder="Name" v-model="fields.payment.card.number">
                        </div>
                        <div class="col-span-2">
                            <label for="">Expiry Month</label>
                            <input v-tilt="{scale: 1.2}" class="input focus:outline-none focus:shadow-outline" type="text" placeholder="Name" v-model="fields.payment.card.expiry_month">
                        </div>
                        <div class="col-span-2">
                            <label for="">Expiry Year</label>
                            <input v-tilt="{scale: 1.2}" class="input focus:outline-none focus:shadow-outline" type="text" placeholder="Name" v-model="fields.payment.card.expiry_year">
                        </div>
                        <div class="col-span-1">
                            <label for="">CVC</label>
                            <input v-tilt="{scale: 1.2}" class="input focus:outline-none focus:shadow-outline" type="text" placeholder="Name" v-model="fields.payment.card.cvc">
                        </div>
                        <div class="col-span-3">
                            <label for="">Billing Zip Code</label>
                            <input v-tilt="{scale: 1.2}" class="input focus:outline-none focus:shadow-outline" type="text" placeholder="Name" v-model="fields.payment.card.postal_zip_code">
                        </div>

                    </div>

                    <div class="grid grid-cols-8 gap-4  justify-items-center content-center px-40 py-10  items-center">
                        <div class="col-span-8 rounded-md bg-gray-800 shadow-lg w-full px-4" style="transform-style: preserve-3d" v-tilt>
                            <div class="grid grid-cols-3 gap-1 border-gray-700 border-b py-4 px-2" v-for="(item, index) in liveObject.line_items" :key="index" :item="item">
                                <div class="col-span-2">
                                    <span class="block text-gray-100">{{item.name}} <b>× {{ item.quantity }}</b></span>
                                </div>
                                <div class="col-span-1 text-right text-green-400">{{item.line_total.formatted_with_symbol}}</div>
                            </div>

                            <div class="grid grid-cols-3 gap-1 text-lg p-4" style="transform: translateZ(20px)">

                                <div class="col-span-2 py-2">
                                    <b class="block text-gray-100">Shipping</b></span>
                                </div>
                                <div class="col-span-1 text-right text-gray-500 py-2">{{liveObject.shipping.price.formatted_with_symbol}}</div>

                                <div class="col-span-2 py-1">
                                    <b class="block text-gray-100">Tax</b></span>
                                </div>
                                <div class="col-span-1 text-right text-gray-500 py-1">{{liveObject.tax.amount.formatted_with_symbol}}</div>

                                <div class="col-span-2">
                                    <b class="block text-gray-100 py-1">Total</b></span>
                                </div>
                                <div class="col-span-1 text-right text-green-500 py-1">{{liveObject.total_with_tax.formatted_with_symbol}}</div>
                            </div>
                        </div>

                        <div class="col-span-8">
                            <a @click="captureCheckout()" class="bg-green-500 cursor-pointer text-white rounded py-5 px-10 shadow-lg buy-button block" style="transform-style: preserve-3d" v-tilt>
                    	    <span  class="block w-full" style="transform: translateZ(20px)"><b>Complete</b> Purchase - $100</span>
                    	  </a>
                        </div>

                    </div>


                </div>
            </div>
        </div>
    </section>
</template>

<script>
import CartItem from './CartItem.vue';
import ConfettiGenerator from "confetti-js";

export default {
    name: 'Checkout',
    props: ['cart', 'merchant', 'checkoutToken'],
    components: {
        CartItem,
    },
    data() {
        return {
            fields: {
                customer: {
                    firstname: 'John',
                    lastname: 'Doe',
                    email: 'john.doe@example.com',
                },
                shipping: {
                    name: 'John Doe',
                    street: '123 Fake St',
                    town_city: 'San Francisco',
                    county_state: 'CA',
                    postal_zip_code: '94103',
                    country: 'US',
                },
                fulfillment: {
                    shipping_method: '',
                },
                payment: {
                    gateway: 'test_gateway',
                    card: {
                        number: '4242 4242 4242 4242',
                        expiry_month: '01',
                        expiry_year: '2023',
                        cvc: '123',
                        postal_zip_code: '94103',
                    },
                },
            },
            shippingOptions: [],
            shippingCountries: [],
            shippingStates: [],
            isCapturing: false,
            message: {
                status: 'alert-danger',
                copy: '',
            },
            liveObject: null,
        };
    },
    watch: {
        checkoutToken() {
            this.generateLiveObject();
            this.getShippingMethods(this.checkoutToken, this.fields.shipping.country);

        },
        selectedCountry() {
            if (this.selectedCountry !== '' && this.selectedCounty !== '') {
                this.getShippingStates(this.checkoutToken, this.fields.shipping.country);
                this.getShippingMethods(this.checkoutToken, this.fields.shipping.country);
            }

        },
        selectedPostal() {
            this.calculateTax(this.fields.shipping);
        },
        selectedCounty() {
            this.calculateTax(this.fields.shipping);
        },
        selectedFullfillment() {
            this.checkShippingMethods(this.fields.fulfillment.shipping_method, this.fields.shipping);
        },
        message: {
            handler() {
                setTimeout(() => {
                    this.message.copy = '';
                }, 10000);
            },
            deep: true,
        },
    },
    computed: {
        selectedCountry() {
            return this.fields.shipping.country;
        },
        selectedPostal() {
            return this.fields.shipping.postal_zip_code;
        },
        selectedCounty() {
            return this.fields.shipping.county_state;
        },
        selectedFullfillment() {
            return this.fields.fulfillment.shipping_method;
        },
    },
    mounted() {
        if (this.checkoutToken == null) {
            return;
        }
        this.generateLiveObject();
        this.getShippingCountries(this.checkoutToken);
        this.getShippingStates(this.checkoutToken, this.fields.shipping.country);
        this.getShippingMethods(this.checkoutToken, this.fields.shipping.country);
        this.confettiNormal();
        return;
    },
    methods: {

        confettiNormal() {
            var confetti = new ConfettiGenerator({ target: 'confetti', max: 100 });
            confetti.render();
        },
        confettiExtreme() {
            var confetti = new ConfettiGenerator({ target: 'confetti', max: 1000, clock: 120 });
            confetti.render();
        },
        /**
         * Gets the available shipping countries
         * https://commercejs.com/docs/sdk/full-sdk-reference#checkout
         *
         * @param {string} Checkout Token
         *
         * @return {object} List of available shipping countries
         */
        getShippingCountries(checkoutToken) {
            this.$commerce.services.localeListShippingCountries(checkoutToken).then((result) => {
                this.shippingCountries = result.countries;
            }).catch((error) => {
                console.error(`Product Error: ${error.message}`);
            });
        },

        /**
         * Gets the available shipping states/provinces
         * https://commercejs.com/docs/sdk/full-sdk-reference#checkout
         *
         * @param {string} Checkout Token
         * @param {object} Selected Country
         *
         * @return {object} List of available shipping states/provinces as defined
         * by the merchant.
         */
        getShippingStates(checkoutToken, country) {
            this.$commerce.services.localeListShippingSubdivisions(checkoutToken, country).then((result) => {
                this.shippingStates = result.subdivisions;
            }).catch((error) => {
                console.error(`Product Error: ${error.message}`);
            });
        },

        /**
         * Gets the available shipping options
         * https://commercejs.com/docs/sdk/full-sdk-reference#checkout
         *
         * @param {string} Checkout Token
         * @param {object} Selected Country
         *
         * @return {object} List of available shipping options as defined
         * by the merchant.
         */
        getShippingMethods(checkoutToken, country) {
            this.$commerce.checkout.getShippingOptions(checkoutToken, { country }).then((result) => {
                this.shippingOptions = result;
            }).catch((error) => {
                console.error(`Product Error: ${error.message}`);
            });
        },
        /**
         * Capture the order and payment.
         * https://commercejs.com/docs/sdk/checkout#capture-order
         *
         * @param {string} Checkout Token.
         * @param {object} Selected products, customer information,shipping information,
         * fullfillment option selected and payment information.
         *
         * @return {object} Order object to be used for reciepts.
         */
        captureCheckout() {

            if(this.fields.fulfillment.shipping_method === ''){
              this.message.copy = 'Please select a shipping method!';
              return;
            }
            //Increase confetti!
            this.confettiExtreme();
            this.isCapturing = true;
            this.$commerce.checkout.capture(
                this.checkoutToken, {
                    line_items: this.lineItemsSanitized(this.cart.line_items),
                    customer: this.fields.customer,
                    shipping: this.fields.shipping,
                    fulfillment: this.fields.fulfillment,
                    payment: this.fields.payment,
                },
            ).then((result) => {
                this.$parent.orderRef = result.customer_reference;
                this.$parent.getCart();
                this.$router.push('/order-confirmation');
            }).catch((error) => {
                this.confettiNormal();
                this.isCapturing = false;
                var firstErrorKey = Object.keys(error.data.error.errors)[0];
                this.message.copy = `${error.data.error.errors[firstErrorKey][0]}`;
            });
        },
        /**
         * Sanitize the line items and get them ready for the order capture.
         */
        lineItemsSanitized(lineItems) {
            return lineItems.reduce((data, lineItem) => {
                const item = data;
                let variantData = null;
                if (lineItem.variants.length) {
                    variantData = {
                        [lineItem.variants[0].variant_id]: lineItem.variants[0].option_id,
                    };
                }
                item[lineItem.id] = {
                    quantity: lineItem.quantity,
                    variants: variantData,
                };
                return item;
            }, {});
        },
        /**
         * Retrieves the live object for use displaying the live cart,
         * shipping, tax and total costs.
         * https://commercejs.com/docs/sdk/checkout#get-the-live-object
         *
         * @param {string} Checkout token.
         *
         * @return {object} Live checkout object.
         */
        generateLiveObject() {
            this.$commerce.checkout.getLive(this.checkoutToken)
                .then((response) => {
                    console.log('liveObject');
                    console.log(response);
                    this.liveObject = response;
                })
                .catch((error) => {
                    this.message.copy = `<strong>${error.data.status_code}</strong>: ${error.data.error.message}`;
                });
        },
        /**
         * Validates the selected shipping method and applies it to the order.
         * https://commercejs.com/docs/sdk/checkout#check-shipping-method
         *
         * @param {string} Shipping option id.
         * @param {string} Country Code eg: US
         * @param {string} Region Code eg: CA
         */
        checkShippingMethods(shippingId, shippingData) {
            this.$commerce.checkout.checkShippingOption(this.checkoutToken, {
                    shipping_option_id: shippingId,
                    country: shippingData.country,
                    region: shippingData.county_state,
                })
                .then(() => {
                    this.generateLiveObject();
                })
                .catch((error) => {
                    this.message.copy = `${error.data.error.message}`;
                });
        },
        /**
         * Sets the tax zone to the order based on location.
         * https://commercejs.com/docs/sdk/checkout#set-tax-zone
         *
         * @param {string} Checkout token.
         * @param {string} Country Code eg: US
         * @param {string} Region Code eg: CA
         * @param {string} Postal/ZIP Code
         *
         * @return {object} Live checkout object.
         */
        calculateTax(shippingData) {
            this.$commerce.checkout.setTaxZone(this.checkoutToken, {
                    country: shippingData.country,
                    region: shippingData.county_state,
                    postal_zip_code: shippingData.postal_zip_code,
                })
                .then(() => {
                    this.generateLiveObject();
                })
                .catch((error) => {
                    this.message.copy = `${error.data.error.message}`;
                });
        },
    },
};
</script>

<style>
body {
    @apply bg-gray-100;
}

input {
    transform: translateZ(20px);
}

.input {
    @apply shadow appearance-none border rounded w-full py-3 px-3 text-gray-700 leading-tight;
    transform: translateZ(20px);
}

label {
    @apply text-gray-600 py-2 block;
}

.loader {
    border-top-color: #ffffff;
    -webkit-animation: spinner 1.5s linear infinite;
    animation: spinner 1.5s linear infinite;
}

@-webkit-keyframes spinner {
    0% {
        -webkit-transform: rotate(0deg);
    }
    100% {
        -webkit-transform: rotate(360deg);
    }
}

@keyframes spinner {
    0% {
        transform: rotate(0deg);
    }
    100% {
        transform: rotate(360deg);
    }
}
</style>
