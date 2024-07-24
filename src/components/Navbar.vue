<template>
  <nav class="navbar navbar-light fixed-top">
    <div class="navbar-text ml-auto d-flex">
      <button class="btn btn-sm btn-outline-success" @click="$emit('toggle')">
        <FontAwesomeIcon icon="fa-solid fa-dollar-sign" />
      </button>
      <div class="dropdown ml-2" v-if="cart.length > 0">
        <button
          class="btn btn-success btn-sm dropdown-toggle"
          id="dropdownCart"
          data-toggle="dropdown"
          aria-haspopup="true"
          aria-expanded="false"
        >
          <span class="badge badge-pill badge-success">{{ cartQty }}</span>
          <FontAwesomeIcon icon="fa-solid fa-shopping-cart mx-2" />
          <price :value="Number(cartTotal)" />
        </button>
        <div
          class="dropdown-menu dropdown-menu-right"
          aria-labelledby="dropdownCart"
        >
          <div v-for="(item, index) in cart" :key="index">
            <div class="dropdown-item-text text-nowrap text-right">
              <span class="badge badge-pill badge-warning align-text-top mr-1">
                {{ item.qty }}
              </span>
              {{ item.product.name }}
              <b>{{ (item.product.price * item.qty) | currencyFormat }}</b>
              <a
                href="#"
                class="badge badge-danger text-white"
                @click.stop="$emit('delete', index)"
                >-</a
              >
            </div>
          </div>
        </div>
      </div>
    </div>
  </nav>
</template>

<script>
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
import Price from "./Price.vue";

export default {
  name: "navbar-layout",
  components: {
    FontAwesomeIcon,
    Price,
  },
  props: ["cart", "cartQty", "cartTotal"],
  filters: {
    currencyFormat: function (value) {
      return "Rp " + Number.parseFloat(value).toFixed(2);
    },
  },
};
</script>
