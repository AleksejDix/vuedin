<template>
  <div class="overflow-hidden">
    <slot></slot>
  </div>
</template>

<script setup lang="ts">
import { reactive, provide } from 'vue'
import { AccordionKey } from './symbols'

const props = defineProps({
  single: {
    type: Boolean,
    default: false,
    required: false
  }
})

const panels = reactive<Record<string, boolean>>({})

function update(id: string, state: boolean) {
  if (props.single) {
    Object.keys(panels).forEach((key) => {
      panels[key] = false
    })
  }
  panels[id] = state
}

function create(id: string, state: boolean) {
  if (panels[id]) return
  panels[id] = state
}

provide(AccordionKey, {
  panels,
  create,
  update
})
</script>
