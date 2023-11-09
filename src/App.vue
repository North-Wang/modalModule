<template>
  <ul class="flex flex-col gap-y-2">
    <li class="flex gap-x-1">
      <button @click="showModal = true">預設</button>
    </li>
    <hr />
    <li class="flex gap-x-1">
      <button @click="showBasicModal = true">有彈窗標題</button>

      <button @click="showTwoButton = true">自訂bodyBottom</button>
      <button @click="showNoButton = true">沒有任何按鈕</button>
    </li>
    <hr />
    <h3 class="text-start">範例</h3>
    <li class="flex gap-x-1">
      <button @click="showThreeColumnModal = true">三欄的彈窗</button>
    </li>
  </ul>

  <Teleport to="body">
    <Modal
      @closeModal="showModal = false"
      @clickButton="showModal = false"
      v-if="showModal"
    >
    </Modal>
  </Teleport>
  <Teleport to="body" v-if="showBasicModal">
    <Modal
      :hasBackIcon="true"
      @closeModal="showBasicModal = false"
      @clickButton="showBasicModal = false"
    >
      <template #headerTitle>
        <div>彈窗的標題</div>
      </template>
      <template #modalContent>
        <div class="text-[#575757]">彈窗的內容</div>
      </template>
    </Modal>
  </Teleport>
  <Teleport to="body" v-if="showTwoButton">
    <Modal :hasBackIcon="true" @closeModal="showTwoButton = false">
      <template #modalContent>
        <ul>
          <li class="font-[18px] text-sky-400 ml-2">劇本測試方法</li>
          <li class="list-align mt-4">
            若您要測試註冊事件，請在此輸入您即將在購物網站要註冊的信箱或電話，該劇本會僅針對您所輸入的信箱做啟用(其他消費者不會被觸發)。
          </li>
          <li class="list-align">
            若您要測試註冊以外的事件，請在此輸入您購物網站已經是會員的信箱或手機，該劇本會僅針對您所輸入的信箱做啟用(其他消費者不會被觸發)。
          </li>
        </ul>
      </template>
      <template #body-bottom>
        <div class="flex justify-end gap-x-2 mt-4">
          <button class="basic-button-light" @click="showTwoButton = false">
            取消
          </button>
          <button class="basic-button" @click="testSignEvent">
            測試註冊事件
          </button>
        </div>
      </template>
    </Modal>
  </Teleport>
  <Teleport to="body" v-if="showNoButton">
    <Modal
      :setModalStyle="{ width: '500px' }"
      :setBodyStyle="{ padding: '30px 16px' }"
      :hasBodyButtonList="false"
      @closeModal="showNoButton = false"
    >
      <template #modalContent>
        <div class="flex justify-center">19:00 君悅酒店柏麗廳 研討會</div>
      </template>
    </Modal>
  </Teleport>
  <Teleport to="body" v-if="showThreeColumnModal">
    <Modal
      :setModalStyle="{ width: '80%' }"
      @closeModal="showThreeColumnModal = false"
    >
      <template #modalContent>
        <ul class="grid grid-cols-3 h-[100px]">
          <li>欄位1</li>
          <li>欄位2</li>
          <li>欄位3</li>
        </ul>
      </template>
    </Modal>
  </Teleport>
</template>

<script setup>
import { ref, Teleport, onMounted } from "vue";
import Modal from "./components/Modal.vue";
import moment from "moment";

const showModal = ref(false);
const showBasicModal = ref(false);
const showTwoButton = ref(false);
const showNoButton = ref(false);
const showThreeColumnModal = ref(false);

const testSignEvent = () => {
  alert("進行測試");
  showTwoButton.value = false;
};
onMounted(() => {});
</script>

<style scoped>
.list-align {
  list-style-type: disc;
  list-style-position: outside;
  margin-left: 25px;
}
</style>
