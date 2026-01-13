<script setup lang="ts">

const props = defineProps<{
  id: number
  name: string
  fill?: boolean
  selected?: boolean
}>()

</script>

<template>
  <div class="bg-yellow-300 rounded-md p-2 flex flex-col cursor-pointer border-2"
    :class="{ 'h-full': fill, 'border-red-500': selected }">
    <p>ID: {{ id }}</p>
    <p>Name: {{ name }}</p>
  </div>
</template>