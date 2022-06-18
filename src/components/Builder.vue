<template>
  <div class="react" id="builder">
    <div class="builder">
      <h3>
        Build your cool Ice Cream
        <span
          class="quantity"
          :style="cart.length === 0 ? { color: 'red' } : {}"
          >{{ cart.length }}</span
        >
      </h3>
      <!-- items start -->
      <div id="items">
        <ul>
          <!-- item start -->
          <li
            class="item"
            :key="variant.id"
            id="item"
            v-for="variant in variants"
          >
            <span>{{ variant.name }}</span>
            <!-- <span class="quantity">2</span> -->
            <div class="right">
              <button
                type="button"
                class="plus rounded"
                @click="handleAddToCart(variant.id)"
              >
                +
              </button>
              <button
                type="button"
                class="minus rounded"
                @click="handleRemoveFromCart(variant.id)"
              >
                -
              </button>
            </div>
          </li>
          <!-- item end -->
        </ul>
      </div>
      <!-- items end -->

      <!-- total price start -->
      <div class="total" id="total">
        <div>Total Price</div>
        <div>{{ total }} Tk</div>
      </div>
      <!-- total price end -->
      <button type="button" @click="toggleModal" class="order rounded">
        Proceed
      </button>
    </div>

    <!-- modal start -->
    <OrderForm
      :cart="cart"
      v-if="showModal"
      @toggle-order-form="toggleModal"
      @clear-cart="$emit('clear-cart')"
      :total="total"
    ></OrderForm>
    <!-- modal end -->
  </div>
</template>

<script>
import OrderForm from "./OrderForm.vue";
export default {
  name: "Builder",
  components: {
    OrderForm,
  },
  data() {
    return {
      showModal: false,
    };
  },
  props: {
    cart: {
      type: Array,
      required: true,
    },
    variants: {
      type: Array,
      required: true,
    },
    total: {
      type: Number,
      required: true,
    },
  },
  methods: {
    handleAddToCart(variantId) {
      this.$emit("add-to-cart", variantId);
    },
    handleRemoveFromCart(variantId) {
      this.$emit("remove-from-cart", variantId);
    },
    toggleModal() {
      this.showModal = !this.showModal;
    },
  },
};
</script>
