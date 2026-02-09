<!--
  NcSteps — Numbered step indicator with connecting lines.
  
  Usage:
    <NcSteps :steps="[
      { title: 'Plan', description: 'Define requirements' },
      { title: 'Build', description: 'Develop MVP', active: true },
      { title: 'Ship', description: 'Deploy to prod' },
    ]" />
-->
<script setup lang="ts">
import { ref, onMounted } from 'vue'

interface Step {
  title: string
  description?: string
  active?: boolean
  done?: boolean
}

defineProps<{
  steps: Step[]
}>()

const visible = ref(false)
onMounted(() => { setTimeout(() => { visible.value = true }, 200) })
</script>

<template>
  <div :class="['nc-steps', { 'nc-steps-visible': visible }]">
    <div
      v-for="(step, i) in steps"
      :key="i"
      :class="['nc-step', { 'nc-step-active': step.active, 'nc-step-done': step.done }]"
      :style="{ '--delay': `${0.15 + i * 0.12}s` }"
    >
      <div class="nc-step-number">
        <span v-if="step.done" class="nc-step-check">✓</span>
        <span v-else>{{ i + 1 }}</span>
        <div v-if="step.active" class="nc-step-ring" />
      </div>
      <div class="nc-step-text">
        <p class="nc-step-title">{{ step.title }}</p>
        <p v-if="step.description" class="nc-step-desc">{{ step.description }}</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.nc-steps {
  display: flex;
  flex-direction: column;
  gap: 0;
}

.nc-step {
  display: flex;
  align-items: flex-start;
  gap: 14px;
  padding: 8px 0;
  position: relative;
  opacity: 0;
  transform: translateX(-12px);
  transition: all 0.5s cubic-bezier(0.16, 1, 0.3, 1);
  transition-delay: var(--delay);
}

.nc-steps-visible .nc-step {
  opacity: 1;
  transform: translateX(0);
}

/* Connector line */
.nc-step:not(:last-child)::after {
  content: '';
  position: absolute;
  left: 15px;
  top: 38px;
  bottom: -8px;
  width: 2px;
  background: rgba(255, 255, 255, 0.06);
}

.nc-step-done:not(:last-child)::after {
  background: rgba(var(--nc-accent-rgb, 227, 6, 19), 0.3);
}

.nc-step-number {
  width: 32px;
  height: 32px;
  min-width: 32px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 0.7rem;
  font-weight: 800;
  color: rgba(255, 255, 255, 0.3);
  background: var(--nc-surface, #161616);
  border: 1px solid rgba(255, 255, 255, 0.08);
  position: relative;
  z-index: 1;
  transition: all 0.3s ease;
}

.nc-step-done .nc-step-number {
  background: var(--nc-accent, #E30613);
  color: white;
  border-color: var(--nc-accent);
  box-shadow: 0 0 15px rgba(var(--nc-accent-rgb, 227, 6, 19), 0.3);
}

.nc-step-active .nc-step-number {
  background: transparent;
  color: white;
  border-color: var(--nc-accent);
  box-shadow: 0 0 20px rgba(var(--nc-accent-rgb, 227, 6, 19), 0.3);
}

.nc-step-ring {
  position: absolute;
  inset: -4px;
  border-radius: 50%;
  border: 2px solid rgba(var(--nc-accent-rgb, 227, 6, 19), 0.3);
  animation: nc-step-ping 2s cubic-bezier(0, 0, 0.2, 1) infinite;
}

@keyframes nc-step-ping {
  0% { transform: scale(1); opacity: 0.5; }
  100% { transform: scale(1.5); opacity: 0; }
}

.nc-step-check {
  font-size: 0.65rem;
}

.nc-step-title {
  font-size: 0.78rem !important;
  font-weight: 700 !important;
  color: white !important;
}

.nc-step-active .nc-step-title {
  color: var(--nc-accent) !important;
}

.nc-step-desc {
  font-size: 0.62rem !important;
  color: rgba(255, 255, 255, 0.35) !important;
  margin-top: 1px;
}
</style>
