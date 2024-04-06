<script setup lang="ts">
import type { InputHTMLAttributes } from 'vue'
import { computed, toRef } from 'vue'
import { useField } from 'vee-validate'


interface BaseInputProps extends /* @vue-ignore */  InputHTMLAttributes {
  name: string
  label?: string
  icon?: string
  id: string
  modelValue: string
}

const props = defineProps<BaseInputProps>()

const { meta, value, errorMessage } = useField(toRef(props, 'name'), undefined, {
  syncVModel: true
})

const hasError = computed(() => errorMessage.value !== undefined && errorMessage.value.length > 0 && meta.touched);

</script>

<template>
  <div class="w-full flex flex-col p-2">
    <div class="font-semibold text-lg">
      <label :for="id">
        {{ label }}
        <span v-if="required">*</span>
        <span class=" text-red-500" v-if="hasError">×</span>
        <span class="dark:text-lime-300 text-lime-500" v-if="meta.valid"> ✓</span>
      </label>
    </div>
    <div class="w-full">

      <input v-bind="props" v-model="value" class="input w-full max-w-xs"
        :class="{ 'input-error': hasError, 'input-success': meta.valid }" />
    </div>
    <small v-if="hasError" class="text-red-500">{{ errorMessage }}</small>
  </div>
</template>
