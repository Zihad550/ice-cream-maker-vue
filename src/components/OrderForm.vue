<template>
  <div id="modal">
    <div class="backdrop" @click="hideOrderForm"></div>
    <div class="modalBody">
      <div class="formContainer" id="orderForm">
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

<style scoped>
.backdrop {
  position: fixed;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.5);
  z-index: 9;
  cursor: pointer;
}

.modalBody {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  -ms-transform: translate(-50%, -50%);
  z-index: 10;
  background-color: white;
}

.formContainer {
  padding: 1rem 3rem;
}
.orderForm {
  max-width: 450px;
  background: #e9ebee;
  padding: 30px;
  margin: 20px auto;
  border-radius: 3px;
}
.orderForm ul {
  padding: 0;
  margin: 0;
  list-style: none;
}
.orderForm ul li {
  display: block;
  margin-bottom: 10px;
  min-height: 35px;
  height: 100%;
  line-height: inherit;
}
.orderForm ul li .fieldStyle {
  box-sizing: border-box;
  padding: 8px;
  outline: none;
  border: 1px solid #dddfe2;
}
.orderForm ul li .fieldStyle:focus {
  box-shadow: 0 0 5px #b0cfe0;
  border: 1px solid #b0cfe0;
}
.orderForm ul li .fieldSplit {
  width: 49%;
}
.orderForm ul li .fieldFull {
  width: 100%;
}
.orderForm ul li input.alignLeft {
  float: left;
}
.orderForm ul li input.alignRight {
  float: right;
}
.orderForm ul li textarea {
  width: 100%;
  height: 100px;
  font-family: inherit;
}

.orderForm ul li input[type="button"],
.orderForm ul li input[type="submit"] {
  background-color: #28a745;
  color: #fff;
  border-color: #28a745;
  border: 1px solid transparent;
  display: block;
  margin: 30px auto 0;
  width: 100%;
  padding: 10px 0;
  font-weight: bold;
  cursor: pointer;
}
</style>
