<template>
  <div>script setup</div>
  <img :src="logo" alt="" />

  <!-- v-memo -->
  <ul>
    <li v-for="item in list" :key="item.id">
      {{ item.title }}
    </li>
  </ul>

  <div class="test">test</div>
  <!-- <van-button type="primary" @click="test">测试</van-button> -->
</template>

<script lang="ts">
export default defineComponent({
  name: 'TestSetupCom',
  inheritAttrs: false,
  customOptions: {}
})
</script>

<script lang="ts" setup>
// import type { test } from "./test"
import logo from '@/assets/logo.png'
import { getCurrentInstance, reactive, ref, defineComponent, onMounted } from 'vue'
import { getNanJing } from '@/api/mock/map'

const props = defineProps({
  msg: String,
  more: {
    type: Object,
    default: () => {}
  }
})

// withDefaults( //TS 类型声明下无法进行设置默认值
//   defineProps<{
//     size?: number
//     labels?: string[]
//   }>(),
//   {
//     a: String,
//     size: 3,
//     labels: () => ['default label']
//   }
// )

interface Ltype {
  name: string
  age: number
}

type c = {
  id: number
  title: string
}

const list = reactive<c[]>([
  { id: 1, title: 'aaa' },
  { id: 2, title: 'aaa2' }
])

const color = ref('red')
const font = reactive({ size: '30px' })

// 声明
const emits = defineEmits(['change', 'delete'])

// TS声明
// const emit = defineEmits<{ (e: 'change', id: number): void; (e: 'update', value: string): void }>()
// // 使用
// emits('change', 1)

function test() {
  console.log('test testSetup', props.msg)
  color.value = 'green'
  font.size = '18px'

  // 使用
  emits('change', font)
}

// var convertData = function (data) {
//   var res = []
//   for (var i = 0; i < data.length; i++) {
//     var geoCoord = mapData[data[i].name]
//     if (geoCoord) {
//       res.push({
//         name: data[i].name,
//         value: geoCoord.concat(data[i].value)
//       })
//     }
//   }
//   return res
// }

defineExpose({ test })

// const attrs = useAttrs()  useCSSModule  useSlots  useCssVars  useTransitionState useSSRContext
</script>

<style lang="scss" scoped>
.test {
  color: v-bind(color);
  font-size: v-bind('font.size');
}
.echarts {
  width: 100%;
  height: 600px;
}
</style>
