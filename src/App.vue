<style scoped>
</style>
<template>
  <template v-if="cloudInfoStore.currentCloud === CloudInfoEnum.cloudAli">
    <div @click="handleOpenDrawerClick" style="display: flex;flex-direction: column;align-items: center">
      <calendar-icon slot="icon" />
      <span @click="handleOpenDrawerClick">分享</span>
    </div>
  </template>
  <template v-else>
    <t-button @click="handleOpenDrawerClick">批量分享操作</t-button>
  </template>

  <t-drawer
      v-model:visible="visible" :header="cloudInfoStore.cloudName" size="600px" :z-index="9999"
:on-confirm="handleClose" @close="handleClose" placement="right" :closeOnOverlayClick="false">
      <component :is="cloudComponent[cloudInfoStore.cloudKey]" ref="operationRef"></component>
  </t-drawer>
</template>


<script setup lang="ts">
//@ts-nocheck
import { CalendarIcon } from 'tdesign-icons-vue-next';
import { ref, shallowRef} from "vue";
import type {Component, Ref,} from "vue"
import {cloudInfoStore} from "./store";
import cloudTianyi from "./components/tianyiCloud/index.vue";
import cloudBaidu from "./components/baiduCloud/index.vue";
import cloudBaiduSync from "./components/baiduCloudSync/index.vue";
import cloud115 from "./components/115Cloud/index.vue";
import cloud123 from "./components/123Cloud/index.vue";
import cloudLanZou from "./components/lanzouCloud/index.vue";
import cloudQuark from "./components/quarkCloud/index.vue";
import cloud139 from "./components/139Cloud/index.vue";
import cloudXun from "./components/xunCloud/index.vue";
import cloudAli from "./components/aliCloud/index.vue";
import cloudUC from "./components/ucCloud/index.vue";
import cloudOnedrive from "./components/onedriveCloud/index.vue";
import {CloudInfoEnum} from "./infoConfig";
export type CloudComponent = {
  [cloudName in keyof typeof CloudInfoEnum]:Component
}
const visible = ref<boolean>(false);
const operationRef = ref();
const cloudComponent:Ref<CloudComponent> = shallowRef({
  cloudTianyi,
  cloudBaidu,
  cloud115,
  cloud123,
  cloudLanZou,
  cloudQuark,
  cloud139,
  cloudXun,
  cloudAli,
  cloudUC,
  cloudOnedrive,
  cloudBaiduSync,
})
//按钮打开
const handleOpenDrawerClick = ():void => {
  visible.value = true;
}
//关闭
const handleClose = ():void => {
  visible.value = false;
  operationRef.value.handleEnd();
}
</script>
