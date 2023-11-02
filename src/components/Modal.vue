<template>
  <transition name="modal">
    <div class="modal-bg">
      <ul
        class="modal-content rounded-lg overflow-hidden"
        ref="target"
        :style="{ width: width, height: height, minHeight: minHeight }"
      >
        <li class="header" v-show="hasHeader">
          <slot name="headerTitle">&nbsp;</slot>
          <img
            :src="Xmark"
            alt="close-modal"
            class="w-2.5 h-2.5 cursor-pointer"
            @click.self="closeModal"
          />
        </li>
        <!-- 內文 -->
        <li class="body p-4">
          <slot name="modalContent"></slot>
        </li>
        <!-- modal footer -->

        <li
          class="footer flex justify-end px-4 pb-4 gap-[24px]"
          v-show="hasFooter"
        >
          <slot name="footer"></slot>
          <button class="basic-button-light" @click="closeModal">
            <slot name="cancel ">取消</slot>
          </button>
          <button class="basic-button" @click="closeModal">
            <slot name="closeModal ">確認</slot>
          </button>
        </li>
      </ul>
    </div>
  </transition>
</template>

<script setup>
import { ref, onMounted, watch, computed, defineEmits, defineProps } from "vue";
import { onClickOutside } from "@vueuse/core";
import Xmark from "../assets/closeModal.svg";

const props = defineProps({
  width: {
    //彈窗寬度
    type: String,
    default: "100%",
  },
  height: {
    //彈窗高度
    type: String,
    default: "",
  },
  minHeight: {
    //彈窗最小高度
    type: String,
    default: "",
  },
  hasHeader: {
    //是否要有header
    type: Boolean,
    default: true,
  },
  hasFooter: {
    //是否要有footer
    type: Boolean,
    default: true,
  },
});
const width = computed(() => {
  return props.width;
});
const height = computed(() => {
  return props.height;
});
const minHeight = computed(() => {
  return props.minHeight;
});
const hasHeader = computed(() => {
  return props.hasHeader;
});
const hasFooter = computed(() => {
  return props.hasFooter;
});
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
  width: 100%;
  background-color: white;
  opacity: 1;
}
.header {
  height: 40px;
  background: var(--unnamed, linear-gradient(90deg, #b5dbe0 0%, #70aeb5 100%));
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 9px 15px;
}
</style>
