<template>
  <Header />
  <div class="mainBody" id="body">
    <div class="container" id="iceCreamBuilder">
      <IceCream :cart="cart" />
      <!-- v-bind:cart = :cart -->
      <Builder
        :cart="cart"
        :variants="variants"
        :total="total"
        @add-to-cart="addToCart"
        @remove-from-cart="removeFromCart"
        @clear-cart="clearCart"
      />
    </div>
  </div>
  <Footer />
</template>

<script>
import Builder from "./components/Builder.vue";
import Footer from "./components/Footer.vue";
import Header from "./components/Header.vue";
import IceCream from "./components/IceCream.vue";
export default {
  name: "App",
  components: {
    Header,
    IceCream,
    Builder,
    Footer,
  },
  data() {
    return {
      variants: [
        {
          id: 1,
          name: "Vanilla",
          price: 100,
        },
        {
          id: 2,
          name: "Chocolate",
          price: 120,
        },
        {
          id: 3,
          name: "Strawberry",
          price: 90,
        },
        {
          id: 4,
          name: "Orange",
          price: 70,
        },
        {
          id: 5,
          name: "Lemon",
          price: 30,
        },
      ],
      cart: [],
    };
  },

  methods: {
    addToCart(variantId) {
      this.cart.push(this.variants.find((variant) => variant.id === variantId));
    },
    removeFromCart(variantId) {
      const position = this.cart.findIndex(
        (variant) => variant.id === variantId
      );
      if (position < 0) return;
      this.cart.splice(position, 1);
    },
    clearCart() {
      this.cart = [];
    },
  },

  computed: {
    total() {
      return this.cart.reduce((total, variant) => total + variant.price, 0);
    },
  },
};
</script>

<style>
/* common */
* {
  box-sizing: border-box;
  font-size: 14px;
  padding: 5px;
}

body {
  margin: 0;
  background: #f3f3f3; /*#53c1de*/
  color: #1d2129;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica,
    Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol";
}

p {
  margin-bottom: 30px;
}

ul {
  list-style-type: none;
  width: 100%;
  margin: 25px auto 10px;
  padding: 0;
}

a,
a:link,
a:visited,
a:hover,
a:active {
  color: #385898;
  text-decoration: none;
}

button {
  outline: none;
  cursor: pointer !important;
}

input[type="submit"]:disabled,
button:disabled {
  opacity: 0.6;
  cursor: not-allowed !important;
}

.right {
  float: right;
}

.textRight {
  text-align: right;
}

.rounded {
  border-radius: 3px;
}

span {
  line-height: normal;
  vertical-align: middle;
  padding: 0;
}

.red {
  color: red;
  padding: 0;
  margin: 0;
}

.container {
  border-bottom: 1px solid #5250507e;
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: 0 auto;
  max-width: 1024px;
}

.container > div {
  width: 100%;
}

/* header */
.logo {
  width: 60px;
}

.vueLogo {
  height: 60px;
  vertical-align: middle;
}

/* main body */

.mainBody {
  margin: 0;
  width: 100%;
  height: 100%;
}

/* icecreamBuilder */
@media only screen and (max-width: 767.99px) {
  .mainBody .container {
    flex-direction: column;
  }
}
</style>
