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

let cpfInputCounter = 0;

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
    const mask = ref('###.###.###-##');
    const generatedId = `input-cpf-${++cpfInputCounter}`;

    const inputId = computed(() => (attrs.id as string) || generatedId);

    return {
      mask,
      inputId,
    };
  },
});
</script>
