<script setup lang="ts">
interface Props {
  id: string
  label: string
  type?: string
  placeholder?: string
}

const { type = 'text', placeholder = '' } = defineProps<Props>()
</script>

<template>
  <div>
    <label :for="id" class="block text-xl">{{ label }}</label>

    <input
      :id
      :type
      :placeholder
      class="mt-2 h-14 w-full rounded-xl border border-neutral-500 bg-neutral-700/50 px-4 text-lg backdrop-blur-md placeholder:text-neutral-300"
    />
  </div>
</template>
