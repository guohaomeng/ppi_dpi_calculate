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

/**
 * 计算并更新设备的每英寸像素（PPI）值及相关显示比例。
 * 该函数没有参数，也不直接返回值，但会更新多个与PPI相关的响应式变量。
 * 
 * 主要步骤包括：
 * 1. 根据屏幕宽度和高度计算对角线上的像素数。
 * 2. 使用对角线像素数除以屏幕尺寸（以英寸为单位）来计算PPI。
 * 3. 更新PPI的字符串表示形式，保留两位小数。
 * 4. 计算并更新基于PPI的缩放百分比，该百分比用于显示调整。
 * 5. 更新缩放百分比的字符串表示形式，不保留小数。
 */
function calculatePPI() {
  // 计算屏幕对角线的像素数
  const diagonalPixels = Math.sqrt(width.value * width.value + height.value * height.value);
  // 根据对角线像素数和屏幕尺寸（英寸）计算PPI
  ppi.value = diagonalPixels / inch.value;
  // 更新PPI的字符串表示
  ppiStr.value = ppi.value.toFixed(2);
  // 计算基于PPI的显示缩放百分比，额外增加PPI除以24的结果（用于基本显示调整）
  scalePercentage.value = ppi.value + Math.round(ppi.value / 24)
  // 更新缩放百分比的字符串表示，不保留小数点后的数字
  scaleStr.value = scalePercentage.value.toFixed(0) + "%"
}
</script>

<style scoped>
#output1::-webkit-scrollbar {
  display: none;
}
</style>