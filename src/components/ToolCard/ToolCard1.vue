<template>
  <n-card title="PPI计算工具" size="small" :segmented="{
    content: true
  }">
    <n-card-content>
      <n-form ref="formRef" inline :label-width="100" size="medium" label-placement="left">
        <n-flex vertical>
          <n-form-item label="屏幕分辨率：">
            <n-input-number v-model:value="width" clearable :precision="0" placeholder="1920" :show-button="true">
              <template #suffix>像素</template></n-input-number>
            <span style="font-size: 1.5em; padding: 0 10px;">×</span>
            <n-input-number v-model:value="height" clearable :precision="0" placeholder="1080" :show-button="true">
              <template #suffix>像素</template></n-input-number>
          </n-form-item>
          <n-form-item label="屏幕尺寸：">
            <n-input-number v-model:value="inch" clearable :precision="2" placeholder="19.53" :step="0.01"
              :show-button="true">
              <template #suffix>英寸</template></n-input-number>
          </n-form-item>
        </n-flex>
      </n-form>
      <n-flex justify="space-around" size="large">
        <n-button @click="calculatePPI" strong secondary type="primary">开始计算PPI</n-button>
      </n-flex>
      <div v-if="inch === 0.00">
        <p>点击按钮开始计算ppi</p>
      </div>
      <div v-else>
        <p>该设备的PPI：{{ ppiStr }}</p>
        <p>适合该设备的缩放比例：{{ scaleStr }}</p>
      </div>
    </n-card-content>
  </n-card>
</template>

<script lang="ts" setup>
import { ref } from "vue";
import { NCard } from 'naive-ui'
import { NButton } from 'naive-ui'
import { NFlex } from 'naive-ui'
import { NInputNumber } from 'naive-ui'
import { NForm } from 'naive-ui'
import { NFormItem } from 'naive-ui'

const width = ref(1920)
const height = ref(1080)
const inch = ref(19.53)
const ppi = ref(0.00)
const scalePercentage = ref(100)
const ppiStr = ref("0.00")
const scaleStr = ref("100")

function calculatePPI() {
  const diagonalPixels = Math.sqrt(width.value * width.value + height.value * height.value);
  ppi.value = diagonalPixels / inch.value;
  ppiStr.value = ppi.value.toFixed(2);
  scalePercentage.value = ppi.value + Math.round(ppi.value / 24)
  scaleStr.value = scalePercentage.value.toFixed(0) + "%"
}
</script>

<style scoped>
#output1::-webkit-scrollbar {
  display: none;
}
</style>