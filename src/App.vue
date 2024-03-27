<template>
  <div id="app" class="container mt-5">
    <h1>IDShop</h1>
    <p class="animate__animated animate__fadeInRight">
      Lorem ipsum dolor sit amet, consectetur adipisicing elit. Aliquam
      aspernatur dolores ea eius eos est facere ipsa ipsum libero magni minus
      nemo nobis, nostrum placeat quis repellat sequi voluptas voluptatem.
    </p>
    <font-awesome-icon icon="shoppingCart"></font-awesome-icon>
  </div>
</template>

<script>
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";

export default {
  name: "App",
  components: {
    FontAwesomeIcon,
  },
};
</script>
