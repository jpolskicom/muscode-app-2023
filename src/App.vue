<template>
  <main class="v-app">
    <h1 class="v-app__title">Muscode App</h1>
    <div class="v-app__content">
      <cTodoList />
      <cProductTable :products="productList" v-on:edit="initEditProduct($event)" />
      <cProductTiles :products="productList" v-on:edit="initEditProduct($event)" />
    </div>
    <cProductEdit
      :product="productEdit"
      v-on:save="saveEditProduct($event)"
      v-on:cancel="cancelEditProduct()"
    />
  </main>
</template>

<script>
import cTodoList from "@/components/TodoList.vue";
import cProductTable from "@/components/ProductTable.vue";
import cProductTiles from "@/components/ProductTiles.vue";
import cProductEdit from "@/components/ProductEdit.vue";

import eTile from "./components/elements/Tile.vue";

export default {
  components: {
    cTodoList,
    cProductEdit,
    cProductTable,
    cProductTiles,
    eTile,
  },
  data() {
    return {
      productEdit: null,
      productList: [
        {
          id: 0,
          title: "iPhone 6s Plus 16GB",
          priceDiscount: 649,
          price: 1000,
          currency: "$",
          image: "/images/img1.png",
        },
        {
          id: 1,
          title: "iPad Pro 32GB",
          priceDiscount: 600,
          price: 800,
          currency: "$",
          image: "/images/img2.png",
        },
        {
          id: 2,
          title: "MacBook Pro",
          priceDiscount: null,
          price: 8000,
          currency: "PLN",
          image: "/images/img3.png",
        },
      ],
    };
  },
  methods: {
    initEditProduct(product) {
      this.productEdit = product;
    },
    cancelEditProduct() {
      this.productEdit = null;
    },
    saveEditProduct(product) {
      this.productList = this.productList.map((e) => (e.id == product.id ? product : e));
      this.cancelEditProduct();
    },
  },
};
</script>

<style lang="scss">
.v-app {
  width: 100%;
  max-width: 1180px;
  margin: 0 auto;
  &__title {
    text-align: center;
    margin: 2rem auto;
  }
  &__content {
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;
    gap: 1rem;
  }
}
</style>
