<template>
  <eTile
    v-for="product in products"
    :key="product.id"
    mode="product"
    :prices="{
      price: product.price,
      priceDiscount: product.priceDiscount,
      currency: product.currency,
    }"
    class="c-productTiles__item"
    v-on:click="$emit('edit', product)"
  >
    <template #title>{{ product.title }}</template>
    <template #content>
      <img
        :src="product.image"
        :alt="`${product.title} | ${
          product.priceDiscount ? product.priceDiscount : product.price
        }${product.currency}`"
      />
    </template>
  </eTile>
</template>
<script>
import eTile from "@/components/elements/Tile.vue";

export default {
  components: {
    eTile,
  },
  props: {
    products: {
      default: () => null,
      type: Array,
    },
  },
};
</script>
<style lang="scss">
.c-productTiles {
  &__item {
    cursor: pointer;
  }
}
</style>
