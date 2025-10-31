<script setup lang="ts">
interface Props {
  id: string
  label: string
  error: string
  type?: string
  placeholder?: string
  autocomplete?: string
}

const { type = 'text', placeholder = '', autocomplete = '' } = defineProps<Props>()

const model = defineModel<string>()
</script>

<template>
  <div>
    <label :for="id" class="block pb-2">{{ label }}</label>

    <input
      :id
      v-model.lazy.trim="model"
      :type
      :placeholder
      :autocomplete
      class="h-14 w-full rounded-xl border border-neutral-500 bg-neutral-700/25 px-4 text-lg outline-offset-2 outline-neutral-500 backdrop-blur-md placeholder:text-neutral-300 hover:bg-neutral-700/75 focus:outline-2"
    />

    <p :class="{ invisible: !error }" class="flex gap-2 py-1 text-xs text-orange-500">
      <img src="../assets/images/icon-error.svg" aria-hidden="true" />
      {{ error ? error : '&nbsp;' }}
    </p>
  </div>
</template>
