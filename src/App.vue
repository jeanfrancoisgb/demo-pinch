<script setup lang="ts">
import '@coddicat/vue-pinch-scroll-zoom/style.css';
import { ref, reactive } from 'vue';
import PinchScrollZoom, {
  type PinchScrollZoomEmitData,
  type PinchScrollZoomExposed
} from '@coddicat/vue-pinch-scroll-zoom';

const state = {
  scale: 1,
  originX: 0,
  originY: 0,
  translateX: 0,
  translateY: 0,
}

const zoomer = ref<PinchScrollZoomExposed>();

function onEvent(name: string, e: PinchScrollZoomEmitData): void {
  // state.eventName = name;
  // state.eventData = e;
  console.log(name, e)
  state.scale = e.scale
  state.originX = e.originX
  state.originY = e.originY
  state.translateX = e.translateX
  state.translateY = e.translateY
}

function zoom() {
  console.log('zoom')
  // console.log(zoomer)
  zoomer.value?.manualZoom({
    factor: 1,
  })
}

function unzoom() {
  // console.log(zoomer)
  console.log('unzoom')

  zoomer.value?.manualZoom({
    factor: -0.5,
  })
}
</script>

<template>
  <div>
    <PinchScrollZoom
      ref="zoomer"
      within
      key-actions
      :width="300"
      :height="400"
      :min-scale="1"
      :max-scale="3"
      @scaling="e => onEvent('scaling', e)"
      @startDrag="e => onEvent('startDrag', e)"
      @stopDrag="e => onEvent('stopDrag', e)"
      @dragging="e => onEvent('dragging', e)"
      style="border: 1px solid black"
      :content-width="2000"
      :content-height="500"
    >
    <div style="width:2000px">
      <img src="https://picsum.photos/500/500" width="500" height="500" />
      <img src="https://picsum.photos/500/500" width="500" height="500" />
      <img src="https://picsum.photos/500/500" width="500" height="500" />
      <img src="https://picsum.photos/500/500" width="500" height="500" />
    </div>
    </PinchScrollZoom>
    <button @click="zoom">Zoom +</button>
    <button @click="unzoom">Zoom -</button>
  </div>
</template>

<style scoped>

</style>
