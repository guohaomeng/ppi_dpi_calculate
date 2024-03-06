<template>
  <n-card title="缩放比与DPI互转工具" size="small" :segmented="{
    content: true
  }">
    <n-card-content>
      <n-form ref="formRef" inline :label-width="100" size="medium" label-placement="left">
        <n-flex vertical>
          <n-form-item label="屏幕缩放比：">
            <n-input-number v-model:value="scalePercentage"  @update:value="scaleToDpi" clearable :precision="0" placeholder="150"
              :show-button="true">

              <template #suffix>%</template></n-input-number>
          </n-form-item>
          <n-form-item label="DPI：">
            <n-input-number v-model:value="dpi" @update:value="dpiToScale" clearable :precision="0" placeholder="144" :step="1"
              :show-button="true"></n-input-number>
          </n-form-item>
        </n-flex>
      </n-form>
      <div class="description">
        <p>DPI = 缩放比 - 四舍五入(缩放比 / 25)</p>
        <p>缩放比 = DPI + 四舍五入(DPI / 24)</p>
        <p>当 DPI = PPI时，屏幕显示比例等于真实值。</p>
        <p>当 DPI > PPI 时，屏幕显示比例大于真实值。</p>
        <p>当 DPI < PPI 时，屏幕显示比例小于真实值。</p>
      </div>
    </n-card-content>
  </n-card>
</template>

<script lang="ts" setup>
import { ref } from "vue";
import { NCard } from 'naive-ui'
import { NFlex } from 'naive-ui'
import { NInputNumber } from 'naive-ui'
import { NForm } from 'naive-ui'
import { NFormItem } from 'naive-ui'

const scalePercentage = ref(150)
const dpi = ref(144)

function scaleToDpi() {
  // 根据缩放比例计算dpi
  dpi.value = scalePercentage.value - Math.round(scalePercentage.value / 25)
}

function dpiToScale() {
  // 根据dpi计算缩放比例
  scalePercentage.value = dpi.value + Math.round(dpi.value / 24);
}
</script>

<style scoped>
#output1::-webkit-scrollbar {
  display: none;
}
</style>