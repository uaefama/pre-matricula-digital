<template>
  <div class="container-sm col-10 col-lg-6 mt-4 pt-lg-4">
    <div class="d-flex align-items-center mb-5">
      <div class="font-muli" style="color: #003473">
        <div style="font-size: 24px">
          {{ getSlogan }}
        </div>
        <h1 class="m-0" style="font-size: 34px; font-weight: inherit">
          {{ getEntityData.city }}
        </h1>
      </div>
      <div class="ml-auto col-5">
        <img :src="getLogo" :alt="getEntityData.city" class="img-fluid" />
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { computed } from 'vue';
import { useGeneralStore } from '@/store/general';

const store = useGeneralStore();

const getEntityData = computed(() => store.getEntityData);
const getSlogan = computed(() => store.getSlogan);
const getLogo = computed(() => store.getLogo);
</script>
