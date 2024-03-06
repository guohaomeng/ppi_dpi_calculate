<template>
    <n-layout position="absolute" style="top: 50px; bottom: 24px" has-sider>
        <n-layout-sider bordered collapse-mode="width" :collapsed-width="64" :width="160" :collapsed="collapsed"
            show-trigger @collapse="collapsed = true" @expand="collapsed = false">
            <n-menu :collapsed="collapsed" :collapsed-width="64" :collapsed-icon-size="22" :options="menuOptions"
                v-model:value="selectedKey" key-field="whateverKey" label-field="whateverLabel"
                children-field="whateverChildren" />
        </n-layout-sider>
        <n-layout :native-scrollbar="false" v-if="selectedKey === 'Home'">
            <div class="mainContent"><MainContent /></div>
        </n-layout>
        <n-layout v-else-if="selectedKey === 'Info'">
            <div class="infoContent"> <InfoContent /> </div>
            
        </n-layout>
        <n-layout v-else>
            <div class="infoContent">错误的菜单项，请检查menuOptions</div>
        </n-layout>
    </n-layout>
</template>
  
<script lang="ts" setup>
import { h, ref, Component } from 'vue'
import { NIcon } from 'naive-ui'
import { NLayout } from 'naive-ui'
import { NLayoutSider } from 'naive-ui'
import { NMenu } from 'naive-ui'
import type { MenuOption } from 'naive-ui'
import {
    Home as HomeIcon,
    InformationCircle as InformationCircleIcon,
    //@ts-ignore
} from '@vicons/ionicons5'
import MainContent from './MainContent.vue'
import InfoContent from './InfoContent.vue'

function renderIcon(icon: Component) {
    return () => h(NIcon, null, { default: () => h(icon) })
}

const menuOptions: MenuOption[] = [
    {
        whateverLabel: '主页',
        whateverKey: 'Home',
        icon: renderIcon(HomeIcon)
    },
    {
        whateverLabel: '关于',
        whateverKey: 'Info',
        icon: renderIcon(InformationCircleIcon)
    }
]

const collapsed = ref(false)
const selectedKey = ref('Home')
</script>
<style>
.mainContent {
    padding: 20px;
}

.infoContent {
    padding: 20px;
}
.n-menu-item-content-header{
    padding-left: 15px;
}
</style>