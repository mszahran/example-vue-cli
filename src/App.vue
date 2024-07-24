<template>
  <div id="app" class="container mt-5">
    <h1>IDShop</h1>
    <navbar
      :cart="cart"
      :cartQty="cartQty"
      :cartTotal="cartTotal"
      @toggle="toggleSliderstatus"
      @delete="deleteItem"
    ></navbar>
    <price-slider
      :slider-status="sliderStatus"
      :maximum.sync="maximum"
    ></price-slider>
    <product-list
      :products="products"
      :maximum="maximum"
      @add="addItem"
    ></product-list>
  </div>
</template>

<script>
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
import PriceSlider from "./components/PriceSlider.vue";
import ProductList from "./components/ProductList.vue";
import Navbar from "./components/Navbar.vue";

export default {
  name: "App",
  data: function () {
    return {
      maximum: 50,
      products: [],
      cart: [],
      sliderStatus: false,
    };
  },
  components: {
    /* eslint-disable-next-line vue/no-unused-components */
    FontAwesomeIcon,
    ProductList,
    PriceSlider,
    Navbar,
  },
  mounted: function () {
    fetch("https://hplussport.com/api/products/order/price")
      .then((response) => response.json())
      .then((data) => {
        this.products = data;
      });
  },
  computed: {
    sliderState: function () {
      return this.style.sliderStatus ? "d-flex" : "d-none";
    },
    cartTotal: function () {
      let sum = 0;
      for (let key in this.cart) {
        // eslint-disable-next-line prettier/prettier
        sum = sum + (this.cart[key].product.price * this.cart[key].qty);
      }
      return sum;
    },
    cartQty: function () {
      let qty = 0;
      for (let key in this.cart) {
        qty = qty + this.cart[key].qty;
      }
      return qty;
    },
  },
  methods: {
    toggleSliderstatus: function () {
      this.sliderStatus = !this.sliderStatus;
    },
    addItem: function (product) {
      let productIndex;
      let productExist = this.cart.filter(function (item, index) {
        if (item.product.id == Number(product.id)) {
          productIndex = index;
          return true;
        } else {
          return false;
        }
      });

      if (productExist.length) {
        this.cart[productIndex].qty++;
      } else {
        this.cart.push({ product: product, qty: 1 });
      }
    },
    deleteItem: function (key) {
      if (this.cart[key].qty > 1) {
        this.cart[key].qty--;
      } else {
        this.cart.splice(key, 1);
      }
    },
  },
};
</script>
