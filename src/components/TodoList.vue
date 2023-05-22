<template>
  <eTile class="c-todoList">
    <template #title>Lista todo</template>
    <template #qty>
      Wykonanie: <CountTo :startVal="0" :endVal="todoListDoneCount" :duration="300" />
    </template>
    <template #content>
      <ul class="c-todoList__list">
        <li
          v-for="item in todoList"
          v-on:click="item.done = !item.done"
          class="c-todoList__list__item"
          :key="item.id"
        >
          <eCheckbox :state="item.done" />
          &nbsp;
          {{ item.value }}
        </li>
      </ul>
      <input
        type="text"
        class="c-todoList__input"
        v-on:keyup.enter="addTodoListElement($event)"
        placeholder="+ Dodaj nowy element checklisty"
      />
    </template>
  </eTile>
</template>
<script>
import { CountTo } from "vue3-count-to";

import eTile from "@/components/elements/Tile.vue";
import eCheckbox from "@/components/elements/Checkbox.vue";

export default {
  components: {
    CountTo,
    eTile,
    eCheckbox,
  },
  data() {
    return {
      todoListElement: {
        id: null,
        value: "",
        done: false,
      },
      todoList: [
        // list items will here
      ],
    };
  },
  computed: {
    todoListDoneCount() {
      return this.todoList.filter((e) => e.done).length;
    },
  },
  methods: {
    addTodoListElement(event) {
      let value = event.target.value;

      if (!value || value == "") {
        window.alert("Nie można dodać pustej wartości!");
        return;
      }

      this.todoList.push({
        ...this.todoListElement,
        value,
        id: this.todoList.length,
      });

      event.target.value = "";
    },
  },
};
</script>
<style lang="scss">
.c-todoList {
  position: relative;
  &__list {
    padding: 0.5rem 0rem;
    &__item {
      border-bottom: 1px solid $borderColor;
      padding: 0.5rem;
      display: flex;
      justify-content: flex-start;
      align-items: center;
      &:hover {
        background-color: $hoverColor;
        cursor: pointer;
        user-select: none;
      }
    }
  }
  &__input {
    font-size: 1rem;
    padding: 0 0.5rem;
    position: sticky;
    bottom: 0;
    left: 0;
    right: 0;
    &::placeholder {
      color: $borderColor;
    }
  }
}
</style>
