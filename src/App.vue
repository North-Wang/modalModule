<template>
  <ul class="flex flex-col gap-y-2">
    <li class="flex gap-x-1">
      <button @click="showModal = true">預設</button>
    </li>
    <hr />
    <li class="flex gap-x-1">
      <button @click="showBasicModal = true">有彈窗標題</button>

      <button @click="showTwoButton = true">兩個按鈕</button>
      <button @click="showFourthButton = true">四個按鈕</button>
      <button @click="showNoButton = true">沒有任何按鈕</button>
    </li>
    <hr />
    <h3 class="text-start">footer的樣式</h3>
    <li class="flex gap-x-1">
      <button @click="showJustifyStart = true">靠左對齊</button>
      <button @click="showJustifyBetween = true">兩側對齊</button>
      <button @click="showJustifyEnd = true">靠右對齊</button>
    </li>
    <li class="flex gap-x-1">
      <button @click="showOneLeftTwoRight = true">左一右二按鈕</button>
    </li>
    <hr />
    <h3 class="text-start">範例</h3>
  </ul>

  <Teleport to="body">
    <Modal
      :width="'398px'"
      @closeModal="showModal = false"
      @clickButton1="showModal = false"
      v-if="showModal"
    >
    </Modal>
  </Teleport>
  <Teleport to="body" v-if="showBasicModal">
    <Modal
      :width="'398px'"
      @closeModal="showBasicModal = false"
      @clickButton1="showBasicModal = false"
    >
      <template #headerTitle>
        <div>彈窗的標題</div>
      </template>
      <template #modalContent>
        <div class="text-[#575757]">發送成功!</div>
      </template>
      <template #button1>確認</template>
    </Modal>
  </Teleport>
  <Teleport to="body" v-if="showTwoButton">
    <Modal
      :width="'398px'"
      :showButton2="true"
      @closeModal="showTwoButton = false"
      @clickButton1="testButton1"
      @clickButton2="testButton2"
    >
      <template #modalContent>
        <ul>
          <li class="font-[18px] text-sky-400">劇本測試方法</li>
          <li class="list-align">
            若您要測試註冊事件，請在此輸入您即將在購物網站要註冊的信箱或電話，該劇本會僅針對您所輸入的信箱做啟用(其他消費者不會被觸發)。
          </li>
          <li class="list-align">
            若您要測試註冊以外的事件，請在此輸入您購物網站已經是會員的信箱或手機，該劇本會僅針對您所輸入的信箱做啟用(其他消費者不會被觸發)。
          </li>
        </ul>
      </template>
      <template #button1>第一個按鈕</template>
      <template #button2>第二個按鈕</template>
    </Modal>
  </Teleport>
  <Teleport to="body" v-if="showFourthButton">
    <Modal
      :width="'600px'"
      :showButton2="true"
      :showButton3="true"
      :showButton4="true"
      :setClassButton1="'basic-button'"
      :setClassButton2="'basic-button-light'"
      :setClassButton3="'basic-button'"
      @closeModal="showFourthButton = false"
      @clickButton1="testButton1"
      @clickButton2="testButton2"
      @clickButton3="testButton3"
      @clickButton4="testButton4"
    >
      <template #modalContent>
        <div style="min-height: 50px">
          確認後仍可編輯投放設定，但寄出前10分鐘內將無法進行任何更改。
        </div>
      </template>
      <template #button1>按鈕1</template>
      <template #button2> 按鈕2 </template>
      <template #button3>按鈕3</template>
      <template #button4>按鈕4</template>
    </Modal>
  </Teleport>
  <Teleport to="body" v-if="showNoButton">
    <Modal
      :width="'500px'"
      :hasFooter="false"
      @closeModal="showNoButton = false"
    >
      <template #modalContent>19:00 君悅酒店柏麗廳</template>
    </Modal>
  </Teleport>
  <Teleport to="body" v-if="showJustifyStart">
    <Modal
      :width="'500px'"
      :showButton2="true"
      :showButton3="true"
      :footerClass="'justify-start'"
      :setClassButton2="'basic-button-light'"
      @closeModal="showJustifyStart = false"
      @clickButton1="showJustifyStart = false"
      @clickButton2="showJustifyStart = false"
    >
      <template #modalContent>已收到信件</template>
    </Modal>
  </Teleport>
  <Teleport to="body" v-if="showJustifyBetween">
    <Modal
      :width="'700px'"
      :showButton2="true"
      :showButton3="true"
      :showButton4="true"
      :footerClass="'justify-between'"
      :setClassButton2="'basic-button-light'"
      @closeModal="showJustifyBetween = false"
      @clickButton1="showJustifyBetween = false"
      @clickButton2="showJustifyBetween = false"
      @clickButton3="showJustifyBetween = false"
      @clickButton4="showJustifyBetween = false"
    >
      <template #modalContent>已收到信件</template>
      <template #button1>按鈕一</template>
      <template #button2>按鈕二</template>
      <template #button3></template>
      <template #button4></template>
    </Modal>
  </Teleport>
  <Teleport to="body" v-if="showJustifyEnd">
    <Modal
      :width="'500px'"
      :showButton2="true"
      :showButton3="true"
      :setClassButton2="'basic-button-light'"
      @closeModal="showJustifyEnd = false"
      @clickButton1="showJustifyEnd = false"
      @clickButton2="showJustifyEnd = false"
    >
      <template #modalContent>已收到信件</template>
    </Modal>
  </Teleport>
  <Teleport to="body" v-if="showOneLeftTwoRight">
    <Modal
      :width="'500px'"
      :showButton2="true"
      :showButton3="true"
      :footerClass="'justify-between'"
      @closeModal="showOneLeftTwoRight = false"
      @clickButton1="showOneLeftTwoRight = false"
      @clickButton2="showOneLeftTwoRight = false"
      @clickButton3="showOneLeftTwoRight = false"
    >
      <template #headerTitle>更改合約內容</template>
      <template #modalContent>請確認內容正確無誤之後送出</template>
      <template #button1>送出</template>
      <template #button3>重新設定</template>
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
const showFourthButton = ref(false);
const showNoButton = ref(false);
const showJustifyStart = ref(false);
const showJustifyBetween = ref(false);
const showJustifyEnd = ref(false);
const showOneLeftTwoRight = ref(false);

const testButton1 = () => [alert("自訂的第一個按鈕事件")];
const testButton2 = () => [alert("自訂的第二個按鈕事件")];
const testButton3 = () => [alert("自訂的第三個按鈕事件")];
const testButton4 = () => [alert("自訂的第四個按鈕事件")];

onMounted(() => {});
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
