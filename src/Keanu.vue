<script setup lang="ts">
import { World, Model, OrbitCamera } from "lingo3d-vue"
import { computed } from "vue"

const props = defineProps({
  quality: String,
})
const quality = computed(() => props.quality)
</script>

<template>
  <div className="w-screen h-screen absolute bg-black flex justify-center items-center">
    <World :performance="quality" defaultLight="studio" color="transparent">
      <Model src="keanu.glb" :scale="5" :metalnessFactor="5" :roughnessFactor="0.5" :boxVisible="false" />
      <OrbitCamera :z="400" active autoRotate enableZoom enablePan enableDamping />
    </World>
  </div>
</template>
