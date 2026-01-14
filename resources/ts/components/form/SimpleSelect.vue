<template>
  <select :id="selectId" v-model="model" v-bind="$attrs">
    <slot name="option" />
    <option v-for="(option, index) in options" :key="index" :value="option.key">
      {{ option.label }}
    </option>
  </select>
</template>

<script lang="ts" setup>
import { computed, useAttrs } from 'vue';
import { ModelValue, Option } from '@/types';
import { useVModel } from '@vueuse/core';

let simpleSelectCounter = 0;

const props = defineProps<{
  modelValue: ModelValue;
  options: Option[];
}>();

const attrs = useAttrs();
const generatedId = `simple-select-${++simpleSelectCounter}`;
const selectId = computed(() => (attrs.id as string) || generatedId);

const model = useVModel(props, 'modelValue');
</script>
