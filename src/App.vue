<template>
  <div class="flex gap-x-1">
    <button @click="showBasicModal = true">基本文字彈窗</button>
    <button @click="showModal = true">劇本提醒</button>
  </div>

  <Teleport to="body" v-if="showBasicModal">
    <Modal :width="'398px'" @closeModal="showBasicModal = false">
      <template #modalContent>
        <div class="text-[#575757]">發送成功!</div>
      </template>
      <template #close-button>確認</template>
    </Modal>
  </Teleport>
  <Teleport to="body" v-if="showModal">
    <Modal :width="'398px'" :hasHeader="true" @closeModal="showModal = false">
      <template #modalContent>
        <div class="text-[18px]">提醒</div>
        <br />
        <div class="text-[14px]">
          <li class="list-align">需先確認觸發管道，並確認已完成串接</li>
          <li class="list-align">
            若測試過程中有任何疑問或需求，煩請與負責窗口聯繫
          </li>
          <li class="flex text-[18px] mt-5 leading-4 items-center font-bold">
            <input
              type="checkbox"
              value="closeModal"
              id="closeModal"
              v-model="notShowModal"
              class="cursor-pointer w-5 h-5"
              @input="changeInput"
            />
            <label for="closeModal" class="cursor-pointer ml-2"
              >今日不再顯示本視窗。</label
            >
          </li>
        </div>
        <!-- <div>發送成功!</div> -->
      </template>
    </Modal>
  </Teleport>
</template>

<script setup>
import { ref, Teleport } from "vue";
import Modal from "./components/Modal.vue";

const showModal = ref(false);
const showBasicModal = ref(false);

const notShowModal = ref(false);

const changeInput = () => {
  console.log("點擊input");
};
</script>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
.list-align {
  list-style-type: disc;
  list-style-position: outside;
  margin-left: 25px;
}
</style>
