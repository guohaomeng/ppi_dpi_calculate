<template>
    <n-grid :x-gap="12" :y-gap="8" cols="1 s:1 m:2 l:2 xl:3 2xl:3" responsive="screen">
        <n-grid-item>
            <ToolCard1 />
        </n-grid-item>
        <n-grid-item>
            <ToolCard2 />
        </n-grid-item>
    </n-grid>
</template>

<script lang="ts" setup>
import { NGrid, NGridItem } from 'naive-ui'
import ToolCard1 from './ToolCard/ToolCard1.vue'
import ToolCard2 from './ToolCard/ToolCard2.vue'
</script>
  
<style>
.light-green {
    height: 108px;
    background-color: rgba(0, 128, 0, 0.12);
    display: flex;
    align-items: center;
    justify-content: center;
}

.green {
    height: 108px;
    background-color: rgba(0, 128, 0, 0.24);
    display: flex;
    align-items: center;
    justify-content: center;
}
.n-card-header__main{
    font-weight: bold !important;
}
</style>