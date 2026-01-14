<template>
  <input
    :id="inputId"
    v-mask="mask"
    v-bind="$attrs"
    type="tel"
    :autocomplete="unique"
  />
</template>

<script lang="ts">
import { PropType, defineComponent, ref, computed, useAttrs } from 'vue';
import { mask } from 'vue-the-mask';

let rgInputCounter = 0;

export default defineComponent({
  directives: {
    mask,
  },
  props: {
    unique: {
      type: String as PropType<string>,
      default: null,
    },
  },
  setup() {
    const attrs = useAttrs();
    const mask = ref('XXX######XXX');
    const generatedId = `input-rg-${++rgInputCounter}`;

    const inputId = computed(() => (attrs.id as string) || generatedId);

    return {
      mask,
      inputId,
    };
  },
});
</script>
