<template>
  <div :class="background">
    <a href="#content" class="skip-to-content">Ir para o conteúdo principal</a>
    <navbar />
    <main id="content" class="container" tabindex="-1">
      <router-view v-slot="{ Component }">
        <transition name="scale" mode="out-in">
          <component :is="Component" />
        </transition>
      </router-view>
    </main>
    <footer id="footer" class="pt-5 pb-5 text-center small">
      © {{ year }} UAEFAMA - União das Escolas Famílias Agrícolas do Maranhão
    </footer>
  </div>
</template>

<script setup lang="ts">
import Navbar from '@/components/elements/Navbar.vue';
import { computed } from 'vue';
import { getFormattedYearFromNow } from '@/datetime';
import { useRoute } from 'vue-router';

const route = useRoute();

const background = computed(() => ({
  'bg-white': !(route.meta.public || false),
}));

const year = computed(() => getFormattedYearFromNow());
</script>

<style scoped>
.skip-to-content {
  position: absolute;
  top: -100%;
  left: 50%;
  transform: translateX(-50%);
  background: #003473;
  color: #fff;
  padding: 0.75rem 1.5rem;
  border-radius: 0 0 0.5rem 0.5rem;
  z-index: 9999;
  text-decoration: none;
  font-weight: bold;
  transition: top 0.2s ease;
}

.skip-to-content:focus {
  top: 0;
  outline: 3px solid #0072ff;
  outline-offset: 2px;
}

.scale-enter-active,
.scale-leave-active {
  transition: all 0.2s ease;
}

.scale-enter-from,
.scale-leave-to {
  opacity: 0;
  transform: scale(0.97);
}
</style>
