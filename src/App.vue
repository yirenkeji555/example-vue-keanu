<script setup lang="ts">
import { usePreload } from "lingo3d-vue"
import { ref, watchEffect } from "vue"
import Keanu from "./Keanu.vue"

const progress = usePreload(["keanu.glb"], "20.5mb")
const quality = ref<"quality" | "balanced" | undefined>(undefined)

const displayFirstScreen = ref<Boolean>(true)
const displayLoading = ref<Boolean>(true)
const displayKeanu = ref<Boolean>(false)

watchEffect(() => {
  if (progress.value > 99) {
    displayLoading.value = false
  }
})
const handleBalanced = (update: "quality" | "balanced") => {
  quality.value = update
  displayFirstScreen.value = false
  displayKeanu.value = true
}
</script>

<template>
  <template v-if="displayFirstScreen">
    <div v-if="displayLoading" class="w-screen h-screen absolute bg-black text-white flex justify-center items-center">
      loading, please wait {{ progress.toFixed(1) }} %
    </div>
    <div v-else className="w-screen h-screen absolute bg-black flex justify-center items-center">
      <button className="mr-3 text-black bg-white px-2 rounded-sm" @click="handleBalanced('balanced')">Speed</button>
      <button className="bg-white text-black px-2 rounded-sm" @click="handleBalanced('quality')">Quality</button>
    </div>
  </template>
  <template v-else>
    <Keanu v-if="displayKeanu" :quality="quality" />
  </template>
</template>
