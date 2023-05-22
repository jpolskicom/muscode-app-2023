<template>
  <button :class="['e-button', `e-button--${mode}`]">
    <slot></slot>
  </button>
</template>
<script>
export default {
  props: {
    mode: {
      // primary,secondary
      default: () => "primary",
      type: String,
    },
  },
};
</script>
<style lang="scss">
.e-button {
  font-size: 1rem;
  padding: 0.25rem 0.5rem;
  margin: 0 0.25rem;
  cursor: pointer;
  &--secondary {
    border: 1px solid $borderColor;
    background-color: white;
    color: $textColor;
    &:hover {
      background-color: $hoverColor;
    }
  }
  &--primary {
    border: 1px solid $borderColor;
    background-color: $selectColor;
    color: $hoverColor;
    &:hover {
      background-color: $hoverColor;
      color: $textColor;
    }
  }
}
</style>
