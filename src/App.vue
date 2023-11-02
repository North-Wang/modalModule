<template>
  <div class="flex gap-x-1">
    <button @click="showBasicModal = true">打開基本文字彈窗</button>
    <button @click="showModal = true">打開彈窗</button>
  </div>

  <Teleport to="body" v-if="showBasicModal">
    <Modal :width="'398px'" @closeModal="showBasicModal = false">
      <template #modalContent> </template>
    </Modal>
  </Teleport>
  <Teleport to="body" v-if="showModal">
    <Modal :width="'398px'" :hasHeader="true" @closeModal="showModal = false">
      <template #modalContent>
        <div class="text-[18px]">自動化劇本提醒</div>
        <br />
        <div class="text-[14px]">
          <li class="list-align">
            需先啟用ReMA功能（Email&手機號碼授權、AWS認證、網域驗證、客戶教育訓練）
          </li>
          <li class="list-align">需先確認觸發管道，並確認已完成串接</li>
          <li class="list-align">
            若測試過程中有任何疑問或需求，煩請與負責窗口聯繫
          </li>
          <li class="list-align">
            劇本中所有寄出信件不屬於系統信，將會受到「行銷名單狀態」的限制，因此信件內容建議放入取消訂閱。
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
