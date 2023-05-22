<template>
  <div :class="['c-tile', `c-tile--${mode}`]">
    <div class="c-tile__percentageDiscount" v-if="percentageDiscount">
      {{ percentageDiscount }}%
    </div>
    <div class="c-tile__header">
      <h2 v-if="$slots.title"><slot name="title" /></h2>
      <h3 v-if="$slots.qty"><slot name="qty" /></h3>
    </div>
    <div class="c-tile__content">
      <span>
        <slot name="content" />
        <template v-if="prices">
          <h4 class="c-tile__price" v-if="prices.price">
            {{ prices.price }} {{ prices.currency }}
          </h4>
          <div class="c-tile__priceDiscount" v-if="prices.priceDiscount">
            {{ prices.priceDiscount }} {{ prices.currency }}
          </div>
        </template>
      </span>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    mode: {
      // Avaible modes: default, large, product
      default: () => "default",
      type: String,
    },
    prices: {
      default: () => null,
    },
  },
  computed: {
    percentageDiscount() {
      return this.prices && this.prices.priceDiscount
        ? Math.round(
            ((this.prices.price - this.prices.priceDiscount) / this.prices.price) * 100
          )
        : null;
    },
  },
};
</script>
<style lang="scss">
.c-tile {
  $t: &;
  padding: 1.5rem;
  border-radius: 1rem;
  box-shadow: 0px -2px 6px 0px $borderColor;
  background-color: white;
  height: 315px;
  position: relative;
  &__header {
    display: flex;
    justify-content: space-between;
  }
  &__content {
    height: 100%;
    max-height: calc(100% - 1.2rem);
    overflow: auto;
  }
  &--default {
    width: 382px;
  }
  &--large {
    width: 782px;
  }
  &--product {
    width: 382px;
    overflow: hidden;
    #{$t}__content {
      padding-top: 1rem;
      display: flex;
      flex-direction: row;
      justify-content: center;
      align-items: center;
      img {
        max-height: 190px;
        object-fit: contain;
      }
    }
  }
  &__price {
    color: $selectColor;
    text-align: center;
  }
  &__priceDiscount {
    text-decoration: line-through;
    text-align: center;
  }
  &__percentageDiscount {
    background: black;
    color: white;
    text-align: center;
    padding: 0.1rem;
    right: -56px;
    top: 10%;
    position: absolute;
    width: 200px;
    transform: rotate(45deg);
  }
}
</style>
