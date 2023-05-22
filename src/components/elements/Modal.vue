slot
<template>
  <div class="e-modal">
    <div class="e-modal__cover" v-on:click="$emit('close', true)"></div>
    <div class="e-modal__container">
      <div class="e-modal__title" v-if="$slots.title">
        <h4>Edycja produktu: <slot name="title"></slot></h4>
      </div>
      <div class="e-modal__content" v-if="$slots.content">
        <slot name="content"></slot>
      </div>
      <div class="e-modal__actions" v-if="$slots.actions">
        <slot name="actions"></slot>
      </div>
    </div>
  </div>
</template>
<style lang="scss">
.e-modal {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  &__cover {
    background-color: rgba(0, 0, 0, 0.5);
    z-index: 888;
    width: 100%;
    height: 100%;
    cursor: pointer;
  }
  &__container {
    z-index: 999;
    position: fixed;
    top: 0;
    bottom: 0;
    right: 0;
    display: flex;
    justify-content: space-between;
    flex-direction: column;
    width: 100%;
    max-width: 585px;
    background-color: white;
    box-shadow: 11px 17px 20px 0px #000000;
  }
  &__title {
    padding: 1.5rem 1rem;
    border-bottom: 3px solid $textColor;
  }
  &__content {
    padding: 1.5rem 1rem;
    height: 100%;
    // display: flex;
    // justify-content: flex-start;
    // align-items: flex-start;
    // flex-direction: column;
  }
  &__actions {
    border-top: 1px solid $borderColor;
    padding: 0.75rem;
  }
}
</style>
