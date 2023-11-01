<template>
  <template ref="target">
    <div id="header" style="width: 100%"></div>
    <slot name="body"> 彈窗內容 </slot>
    <slot name="footer"></slot>
  </template>
</template>

<script setup>
import { ref, onMounted, watch, defineEmits } from "vue";
import { onClickOutside } from "@vueuse/core";

const emits = defineEmits(["closeModal"]);

const target = ref(null);
onClickOutside(target, () => {
  closeModal();
});

const closeModal = () => {
  emits("closeModal");
};
</script>

<style scoped></style>
