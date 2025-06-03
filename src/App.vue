<template>
  <div class="segment-demo">
    <div class="segment">
      <button
        class="segment-button"
        :class="{ 'is-active': activeSegment === 'page-a' }"
        @click="activeSegment = 'page-a'"
        type="button"
      >
        Page A
      </button>
      <button
        class="segment-button"
        :class="{ 'is-active': activeSegment === 'page-b' }"
        @click="activeSegment = 'page-b'"
        type="button"
      >
        Page B
      </button>
      <button
        class="segment-button"
        :class="{ 'is-active': activeSegment === 'page-c' }"
        @click="activeSegment = 'page-c'"
        type="button"
      >
        Page C
      </button>
    </div>

    <KeepAlive>
      <component :is="currentPage" />
    </KeepAlive>
  </div>
</template>

<script setup lang="ts">
import { computed, ref } from 'vue'
import PageA from './pages/PageA.vue'
import PageB from './pages/PageB.vue'
import PageC from './pages/PageC.vue'

const activeSegment = ref<'page-a' | 'page-b' | 'page-c'>('page-a')

const pages = {
  'page-a': PageA,
  'page-b': PageB,
  'page-c': PageC,
}

const currentPage = computed(() => pages[activeSegment.value])
</script>

<style scoped>
.segment-demo {
  font-family: system-ui, sans-serif;
  color: white;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  width: 90vw;
  height: 90vh;
  gap: 16px;
  padding: 24px 0;
}

.segment {
  display: flex;
  background: rgba(90, 90, 90, 0.44);
  border-radius: 8px;
  box-shadow: 0 1px 2px rgba(30, 34, 40, 0.04);
  user-select: none;
}

.segment-button {
  border: none;
  width: 8rem;
  height: 2rem;
  color: #fff;
  background: rgba(20, 20, 20, 0.2);
  font-weight: 500;
  border-radius: 8px;
  cursor: pointer;
  transition:
    background 0.2s,
    color 0.2s;
  outline: none;
  font-size: 1rem;
  margin: 0;
  position: relative;
}

.segment-button:not(:last-child) {
  margin-right: 4px;
}

.segment-button.is-active {
  background: #666;
  box-shadow: 0 2px 8px rgba(25, 118, 210, 0.04);
}

.segment-button:active:not(.is-active) {
  background: #d4dae0;
}

.segment-button:focus-visible {
  outline: 2px solid #1976d2;
  outline-offset: 2px;
}

@media (max-width: 600px) {
  .segment {
    flex-wrap: wrap;
  }
  .segment-button {
    padding: 8px 12px;
    font-size: 0.95rem;
  }
}
</style>
