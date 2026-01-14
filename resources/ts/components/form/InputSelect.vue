<template>
  <select :id="selectId" v-model="model" v-bind="$attrs">
    <option v-for="option in options" :key="option.id" :value="option.id">
      {{ option.label }}
    </option>
  </select>
</template>

<script lang="ts">
import { PropType, defineComponent, computed, useAttrs } from 'vue';
import { useVModel } from '@vueuse/core';

let inputSelectCounter = 0;

export default defineComponent({
  props: {
    modelValue: {
      type: String as PropType<string>,
      default: null,
    },
    options: {
      type: Array as PropType<{ id: string; label: string }[]>,
      default: () => [],
    },
  },
  emits: ['input'],
  setup(props) {
    const attrs = useAttrs();
    const model = useVModel(props, 'modelValue');
    const generatedId = `input-select-${++inputSelectCounter}`;
    const selectId = computed(() => (attrs.id as string) || generatedId);

    return {
      model,
      selectId,
    };
  },
});
</script>
