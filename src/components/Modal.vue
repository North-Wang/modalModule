<template>
  <div class="modal-bg">
    <transition name="slide-fade">
      <ul
        class="modal-content rounded-lg overflow-hidden"
        ref="target"
        :style="setModalStyle"
        role="dialog"
        aria-labelledby="modalTitle"
        aria-describedby="modalDescription"
        v-show="showModal"
      >
        <li class="header" v-show="hasHeader">
          <div class="flex items-center">
            <img
              :src="goBackIcon"
              alt="go-back-icon"
              class="w-2.5 h-2.5 cursor-pointer mr-2"
              @click.self="closeModal"
              v-show="hasBackIcon"
            />
            <div class="text-white" :style="setHeaderTitleStyle">
              <slot name="headerTitle"></slot>
            </div>
          </div>

          <img
            :src="Xmark"
            alt="close-modal"
            class="w-2.5 h-2.5 cursor-pointer"
            @click.self="closeModal"
            v-show="hasXMark"
          />
        </li>
        <!-- body -->
        <li class="body flex flex-col" :style="setBodyStyle">
          <slot name="modalContent"></slot>
          <!-- default button -->
          <slot name="body-bottom">
            <div :style="setBodyBottom" v-if="hasBodyButtonList">
              <button
                class="basic-button"
                :style="setButtonStyle"
                @click.self="clickButton"
              >
                確認
              </button>
            </div>
          </slot>
        </li>
        <!-- footer -->
        <li class="footer" v-if="hasFooter">
          <slot name="footer">
            <div class="footer-default-content">footer default content</div>
          </slot>
        </li>
      </ul>
    </transition>
  </div>
</template>

<script setup>
import { ref, onMounted, watch, computed, defineEmits, defineProps } from "vue";
import { onClickOutside } from "@vueuse/core";
import Xmark from "../assets/closeModal.svg";
import goBackIcon from "../assets/goBackIcon.svg";

const props = defineProps({
  /* ----- 與元件顯示相關 start ----- */
  hasHeader: {
    type: Boolean,
    default: true,
  },
  hasBackIcon: {
    //標頭左側的關閉彈窗icon
    type: Boolean,
    default: false,
  },
  hasXMark: {
    //標頭右側的關閉彈窗icon
    type: Boolean,
    default: true,
  },
  hasBodyButtonList: {
    //是否顯示body下方的按鈕列
    type: Boolean,
    default: true,
  },
  hasFooter: {
    type: Boolean,
    default: false,
  },

  /* ----- 與元件顯示相關 end ----- */

  /* ----- 修改style start ----- */
  //彈窗本身
  setModalStyle: {
    type: Object,
    default: () => ({
      width: "50%",
    }),
  },
  //標頭的標題
  setHeaderTitleStyle: {
    type: Object,
    default: () => ({}),
  },
  //彈窗內容的style
  setBodyStyle: {
    type: Object,
    default: () => ({
      padding: "1rem",
    }),
  },
  setButtonStyle: {
    type: Object,
    default: () => ({}),
  },
  setBodyBottom: {
    type: Object,
    default: () => ({
      justifyContent: "end",
      marginTop: "25px",
      display: "flex",
    }),
  },
  /* ----- 修改style end ----- */
});
const emits = defineEmits(["closeModal"]);

const target = ref(null);
onClickOutside(target, (e) => {
  closeModal();
});
const showModal = ref(false);
const closeModal = () => {
  //關閉彈窗
  showModal.value = false;
  setTimeout(() => {
    emits("closeModal");
  }, 400);
};
const clickButton = () => {
  closeModal();
};

onMounted(() => {
  showModal.value = true;
});
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
  font-family: "Franklin Gothic Medium", "Arial Narrow", Arial, sans-serif;
}
.modal-content {
  width: 100%;
  background-color: white;
  opacity: 1;
  display: flex;
  flex-direction: column;
}
.header {
  height: 30px;
  background: var(--unnamed, linear-gradient(90deg, #b5dbe0 0%, #70aeb5 100%));
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 9px 15px;
}
.footer-default-content {
  display: flex;
  flex-direction: column;
  width: 100%;
  justify-content: center;
  text-align: center;
  padding: 12px;
}
/* 進場動畫 */
.slide-fade-enter-active {
  transition: all 0.3s ease-out;
  transition-delay: 0.1s;
}

.slide-fade-leave-active {
  transition: all 0.2s linear;
  transition-delay: 0.1s;
}

.slide-fade-enter-from,
.slide-fade-leave-to {
  transform: translateY(-30px);
  opacity: 0;
}
</style>
