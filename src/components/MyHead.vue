<script lang="ts" setup>
import { ref } from "vue";
import { NSwitch } from 'naive-ui'
import { NForm } from 'naive-ui'
import { NFormItem } from 'naive-ui'
import { NLayoutHeader } from 'naive-ui'

const active = ref(false)


</script>

<template>
    <n-layout-header bordered>
        <div class="headMain">
            <div class="headLeft">
                <!-- <n-avatar size="large" src="/logo.png" object-fit="fill" /> -->
            </div>
            <div class="headCenter">
                <h1>PPI/DPI计算工具箱</h1>
            </div>
            <div class="headRight">
                <n-form label-placement="left" label-width="auto" :show-feedback="false">
                    <n-form-item label="深色模式">
                        <n-switch v-model:value="active" @update:value="$emit('themeChange', active)" size="small">
                            <template #checked>开</template>
                            <template #unchecked>关</template>
                        </n-switch>
                    </n-form-item>
                </n-form>
            </div>
        </div>
    </n-layout-header>
</template>

<style>
h1 {
    font-size: 20px;
    line-height: 1em;
    text-align: center;
}

.headMain {
    width: 100%;
    height: auto;
    display: flex;
    align-items: center;
    justify-content: space-evenly;
}

.headLeft {
    width: 15%;
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: space-between;
}

.headCenter {
    width: 50%;
    height: 100%;
    align-items: center;
}

.headRight {
    width: 15%;
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: right;
}
</style>