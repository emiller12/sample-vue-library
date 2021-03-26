<template>
  <div @click="toggleDropDown" class="dropdown">
    <slot name="title">
      <div class="dropdown__title">
        {{ title }}
        <svg
            class="dropdown__icon"
            :class="{ 'dropdown__icon-up': isOpen }"
            xmlns="http://www.w3.org/2000/svg"
            viewBox="0 0 20 20"
            fill="currentColor"
            aria-hidden="true"
        >
          <path
              fill-rule="evenodd"
              d="M7.293 14.707a1 1 0 010-1.414L10.586 10 7.293 6.707a1 1 0 011.414-1.414l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414 0z"
              clip-rule="evenodd"
          />
        </svg>
      </div>
    </slot>

    <ul
        v-show="isOpen"
        ref="menu"
        :class="['dropdown__menu']"
    >
      <slot />
    </ul>
  </div>
</template>

<script lang="ts">

import { defineComponent, ref } from "@vue/composition-api";

export default defineComponent({
  name: "dropdown",
  props: {
    title: {
      type: String,
      default: ""
    }
  },
  setup() {
    const isOpen = ref(false);

    function toggleDropDown() {
      isOpen.value = !isOpen.value;
    }

    function closeDropDown() {
      isOpen.value = false;
    }

    return { isOpen, toggleDropDown, closeDropDown };
  }
});
</script>

<style scoped>
.dropdown__icon {
  height: 1.25rem;
  width: 1.25rem;
  transform: rotate(90deg);
  color: darkgray;
  margin-left: 20px;
}

.dropdown__icon-up {
   transform: rotate(-90deg);
 }

.dropdown__menu {
   background-color: whitesmoke;
   min-width: 160px;
   box-shadow: 0 8px 16px 0 rgba(0, 0, 0, 0.2);
   z-index: 1;
   list-style-type: none;
   max-height: 250px;
   overflow-y: scroll;
   margin-top: 5px;
   border-radius: 4px;
 }

.dropdown__menu li {
   cursor: pointer;
   padding: 10px;
   font-size: 14px;
 }

.dropdown__menu li:hover,
 li.selected {
   background-color: lightgray;
 }
</style>
