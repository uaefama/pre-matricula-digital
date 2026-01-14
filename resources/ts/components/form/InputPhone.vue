<template>
  <input
    :id="inputId"
    v-mask="mask"
    v-bind="$attrs"
    :value="model"
    type="tel"
    :autocomplete="unique"
  />
</template>

<script lang="ts">
import { PropType, defineComponent, ref, computed, useAttrs } from 'vue';
import { ModelValue } from '@/types';
import { mask } from 'vue-the-mask';
import { useVModel } from '@vueuse/core';

let phoneInputCounter = 0;

export default defineComponent({
  directives: {
    mask,
  },
  props: {
    data: {
      type: String as PropType<ModelValue>,
      default: null,
    },
    unique: {
      type: String as PropType<string>,
      default: null,
    },
  },
  setup(props) {
    const attrs = useAttrs();
    const mask = ref(['(##) ####-####', '(##) #####-####']);
    const generatedId = `input-phone-${++phoneInputCounter}`;

    const inputId = computed(() => (attrs.id as string) || generatedId);
    const model = useVModel(props, 'data');

    return {
      mask,
      model,
      inputId,
    };
  },
});
</script>
