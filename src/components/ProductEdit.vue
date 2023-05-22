<template>
  <eModal v-if="product" v-on:close="$emit('cancel')" class="c-productEdit">
    <template #title>
      {{ product.title }}
    </template>
    <template #content>
      <div class="c-productEdit__image">
        <img :src="productEdit.image" :alt="productEdit.title" />
      </div>
      <label>
        Nazwa produktu
        <input type="text" v-model="productEdit.title" />
      </label>
      <label>
        Cena
        <input type="number" v-model="productEdit.price" />
      </label>
      <label>
        Promocyjna cena
        <input type="number" v-model="productEdit.priceDiscount" />
      </label>
      <label>
        Waluta
        <select v-model="productEdit.currency">
          <option v-for="currency in currencies" :key="currency">
            {{ currency }}
          </option>
        </select>
      </label>
    </template>
    <template #actions>
      <eButton mode="primary" v-on:click="$emit('save', productEdit)">Zapisz</eButton>
      <eButton mode="secondary" v-on:click="$emit('cancel')">Anuluj</eButton>
    </template>
  </eModal>
</template>
<script>
import eModal from "@/components/elements/Modal.vue";
import eButton from "@/components/elements/Button.vue";

export default {
  components: {
    eModal,
    eButton,
  },
  data() {
    return {
      productEdit: null,
      currencies: ["$", "PLN"],
    };
  },
  props: {
    product: {
      default: () => null,
      type: Object || null,
    },
  },
  watch: {
    product: {
      handler() {
        this.productEdit = { ...this.product };
      },
      deep: true,
    },
  },
};
</script>
<style lang="scss">
.c-productEdit {
  &__image {
    width: 205px;
    height: 205px;
    margin: 2rem auto;
    border-radius: 205px;
    overflow: hidden;
    box-shadow: 1px -1px 13px -10px #000000;
    display: flex;
    justify-content: center;
    align-items: center;
    img {
      width: 70%;
      height: 70%;
      object-fit: contain;
    }
  }
}
</style>
