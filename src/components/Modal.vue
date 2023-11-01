<template>
  <div class="modal-bg">
    <div class="modal-content" ref="target">
      <div id="header" style="width: 100%"></div>
      <slot name="body"> 彈窗內容 </slot>
      <slot name="footer"></slot>
    </div>
  </div>
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

<style scoped>
.modal-bg {
  width: 100vw;
  height: 100vh;
  background-color: rgb(0, 0, 0, 0.4);
  position: absolute;
  z-index: 100;
  display: flex;
  justify-content: center;
  align-items: center;
}
.modal-content {
  width: 100px;
  height: 500px;
  background-color: white;
  opacity: 1;
}
</style>
