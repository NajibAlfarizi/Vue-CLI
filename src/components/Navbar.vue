<template>
  <nav class="navbar navbar-light fixed-top">
    <div class="navbar-text ml-auto d-flex">
      <button
        class="btn btn-sm btn-outline-success"
        @click="$emit('toggle-slide')"
      >
        <font-awesome-icon icon="dollar-sign"></font-awesome-icon>
      </button>
      <div class="dropdown ml-2" v-if="cart.length > 0">
        <button
          class="btn btn-success btn-sm dropdown-toggle"
          id="dropdownCart"
          data-toggle="dropdown"
          aria-haspopup="true"
          aria-expanded="false"
        >
          <span class="badge badge-pill badge-light">{{ cartQty }}</span>
          <i class="fas fa-shopping-cart mx-2"></i>
          <font-awesome-icon icon="shopping-cart"></font-awesome-icon>
          <price :value="Number(cartTotal)"></price>
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
              <b>{{ (item.qty * item.product.price) | currencyFormat }}</b>
              <a
                href="#"
                class="badge badge-danger text-white"
                @click.stop="$emit('delete-item', index)"
                >-</a
              >
            </div>
          </div>
          <router-link
            class="btn btn-sm btn-info btn-outline-dark text-white float-right mr-2"
            to="/chekout"
          >
            Checkout
          </router-link>
        </div>
      </div>
    </div>
  </nav>
</template>

<script>
import Price from "./Price.vue";
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";

export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "navbar",
  props: ["cart", "cartQty", "cartTotal"],
  components: {
    Price,
    FontAwesomeIcon,
  },
  filters: {
    currencyFormat: function (value) {
      return "Rp" + Number.parseFloat(value).toFixed(2);
    },
  },
};
</script>
