<script setup lang="ts">
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup
import { ref } from "vue";
import myHead from './components/MyHead.vue'
import MySider from './components/MySider.vue'
import MyFooter from './components/MyFooter.vue';
import { darkTheme } from "naive-ui";
import { lightTheme } from "naive-ui";
import { NConfigProvider } from 'naive-ui'
import { NGlobalStyle } from 'naive-ui'
import { NLayout } from 'naive-ui'
import { NMessageProvider } from 'naive-ui'

const theme = ref(lightTheme); //主题变量

</script>

<template>
  <n-message-provider>
    <n-config-provider :theme="theme">
      <n-layout style="height: 100vh">
        <div class="container">
          <div class="header">
            <myHead @themeChange="(mode) => mode == true ? theme = darkTheme : theme = lightTheme" />
          </div>
          <div class="content">
            <MySider />
          </div>
          <div class="footer">
            <MyFooter />
          </div>
        </div>
      </n-layout>
      <n-global-style />
    </n-config-provider>
  </n-message-provider>
</template>

<style>
.container {
  background-color: var(--n-color);
  max-width: 100%;
  margin: 2px;
  padding: 0;

  /* border-left: 2px solid #ebeef5;
  border-right: 2px solid #ebeef5;
  border-radius: 5px; */
}

.header {
  width: 100%;
  height: 50px;
  /* background-color: #fff;
  border-bottom: 1px solid #ebeef5;
  box-shadow: 0 2px 4px 0 rgba(0, 0, 0, .12); */
}

.content {
  width: 100%;
  height: 100%;
  /* background-color: #fff;
  border-bottom: 1px solid #ebeef5;
  box-shadow: 0 2px 4px 0 rgba(0, 0, 0, .12); */
}
</style>