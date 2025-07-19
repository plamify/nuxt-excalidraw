<script setup lang="ts">
import type { ExcalidrawProps } from '@excalidraw/excalidraw/types/types'
import type { Ref } from 'vue'
import React from 'react'
import { nextTick, onMounted, ref } from 'vue'

export interface Props extends /* @vue-ignore */ ExcalidrawProps {}

const props = defineProps<Props>()

const excalidrawRef: Ref<HTMLDivElement | null> = ref(null)

onMounted(() => {
  nextTick(async () => {
    if (excalidrawRef.value) {
      const { Excalidraw } = await import('@excalidraw/excalidraw')
      const { createRoot } = await import('react-dom/client')

      const root = createRoot(excalidrawRef.value)
      root.render(
        React.createElement(Excalidraw, props as any),
      )
    }
  })
})
</script>

<template>
  <div ref="excalidrawRef" class="excalidraw-board" />
</template>

<style scoped>
.excalidraw-board {
  min-height: 100%;
  height: 90dvh;
}
</style>
