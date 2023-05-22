<template>
  <eTile mode="large" v-if="products" class="c-productTable">
    <template #title>Lista produktów</template>
    <template #content>
      <table>
        <thead>
          <tr>
            <th>#</th>
            <th>Nazwa</th>
            <th>Promocyjna cena</th>
            <th>Cena</th>
            <th>Waluta</th>
          </tr>
        </thead>
        <tbody>
          <tr
            v-for="product in products"
            :key="product.id"
            v-on:click="$emit('edit', product)"
            class="c-productTable__item"
          >
            <td>{{ product.id }}</td>
            <td>{{ product.title }}</td>
            <td>{{ product.priceDiscount }}</td>
            <td>{{ product.price }}</td>
            <td>{{ product.currency }}</td>
          </tr>
        </tbody>
      </table>
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
.c-productTable {
  table {
    margin-top: 1rem;
  }
  td,
  th {
    padding: 0.5rem;
  }
  th {
    text-transform: uppercase;
  }
  &__item {
    cursor: pointer;
    border-bottom: 1px solid $borderColor;
  }
}
</style>
