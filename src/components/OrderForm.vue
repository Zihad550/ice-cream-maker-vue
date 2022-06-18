<template>
  <div id="modal">
    <div class="backdrop" @click="hideOrderForm"></div>
    <div class="modalBody">
      <div class="formContainer react" id="orderForm">
        <h1>Complete the form below and hit submit</h1>
        <form class="orderForm" @submit.prevent="onSubmit">
          <ul>
            <li>
              <input
                type="text"
                v-model="name"
                class="fieldStyle fieldSplit alignLeft"
                placeholder="Name"
              />
              <input
                type="text"
                v-model="phone"
                class="fieldStyle fieldSplit alignRight"
                placeholder="Phone no."
              />
              <input
                type="hidden"
                v-model.number="total"
                class="fieldStyle fieldSplit alignRight"
              />
            </li>
            <li>
              <input
                type="text"
                v-model="email"
                class="fieldStyle fieldFull"
                placeholder="Email"
              />
            </li>
            <li>
              <textarea
                v-model="address"
                class="fieldStyle"
                placeholder="Address"
              ></textarea>
            </li>
            <li>
              <input type="submit" value="Submit Order" />
            </li>
          </ul>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "OrderForm",
  props: {
    total: {
      type: Number,
      required: true,
    },
    cart: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      name: "",
      email: "",
      phone: "",
      address: "",
    };
  },
  methods: {
    onSubmit() {
      const orderDetails = {
        name: this.name,
        email: this.email,
        phone: this.phone,
        address: this.address,
        total: this.total,
      };
      console.log(orderDetails);
      this.$emit("clear-cart");
      this.hideOrderForm();
    },

    hideOrderForm() {
      this.$emit("toggle-order-form");
    },
  },
};
</script>
