<template>
  <transition-group
    name="fade"
    tag="div"
    @beforeEnter="beforeEnter"
    @enter="enter"
    @leave="leave"
  >
    <div
      class="row d-flex mb-3 align-items-center"
      v-for="(item, index) in products"
      :key="item.id"
      v-if="item.price <= Number(maximum)"
      :data-index="index"
    >
      <div class="col-2 m-auto">
        <button class="btn btn-info" @click="$parent.$emit('add', item)">
          Add to Cart
        </button>
      </div>
      <div class="col-4">
        <img class="img-fluid d-block" :src="item.image" :alt="item.name" />
      </div>
      <div class="col">
        <router-link :to="'/product-detail/' + item.id"
          ><h3 class="text-info">{{ item.name }}</h3></router-link
        >
        <p class="mb-0">{{ item.description }}</p>
        <div class="h5 float-right">
          <price :value="Number(item.price)"> </price>
        </div>
      </div>
    </div>
  </transition-group>
</template>

<script>
import Price from "./Price.vue";
export default {
  name: "product-list",
  components: { Price },
  props: ["products", "maximum"],
  methods: {
    beforeEnter: function(el) {
      el.className = "d-none";
    },
    enter: function(el) {
      var delay = el.dataset.index * 50;
      setTimeout(() => {
        el.className =
          "row d-flex mb-3 align-items-center animated fadeInRight ";
      }, delay);
    },
    leave: function(el) {
      var delay = el.dataset.index * 10;
      setTimeout(() => {
        el.className =
          "row d-flex mb-3 align-items-center animated fadeOutRight ";
      }, delay);
    }
  }
};
</script>
