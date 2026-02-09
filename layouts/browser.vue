<!--
  NeοCarbon — Browser Layout
  Content rendered inside a Safari/Chrome browser frame with URL bar.
  Great for showcasing web apps, dashboards, or websites.

  Usage:
    ---
    layout: browser
    url: https://app.example.com/dashboard
    ---
    # Dashboard content inside browser frame
-->
<script setup lang="ts">
defineProps<{
  url?: string
}>()
</script>

<template>
  <div class="slidev-layout nc-browser nc-custom-layout">
    <div class="nc-browser-frame">
      <div class="nc-browser-toolbar">
        <div class="nc-browser-dots">
          <span class="nc-bdot nc-bdot-r" />
          <span class="nc-bdot nc-bdot-y" />
          <span class="nc-bdot nc-bdot-g" />
        </div>
        <div class="nc-browser-url">
          <svg class="nc-lock-icon" viewBox="0 0 16 16" fill="currentColor" width="10" height="10">
            <path d="M8 1a3 3 0 0 0-3 3v2H4a1 1 0 0 0-1 1v6a1 1 0 0 0 1 1h8a1 1 0 0 0 1-1V7a1 1 0 0 0-1-1h-1V4a3 3 0 0 0-3-3zm-1.5 3a1.5 1.5 0 1 1 3 0v2h-3V4z"/>
          </svg>
          <span>{{ url || 'https://example.com' }}</span>
        </div>
        <div class="nc-browser-actions">
          <span class="nc-browser-btn">⟨</span>
          <span class="nc-browser-btn">⟩</span>
          <span class="nc-browser-btn">↻</span>
        </div>
      </div>
      <div class="nc-browser-body">
        <slot />
      </div>
    </div>
  </div>
</template>

<style scoped>
.nc-browser {
  display: flex !important;
  flex-direction: column !important;
  height: 100%;
  padding: 1.2rem 2rem !important;
}

.nc-browser-frame {
  flex: 1;
  display: flex;
  flex-direction: column;
  border-radius: 12px;
  overflow: hidden;
  border: 1px solid rgba(255, 255, 255, 0.1);
  box-shadow:
    0 25px 80px rgba(0, 0, 0, 0.5),
    0 0 1px rgba(255, 255, 255, 0.1);
  animation: nc-browser-enter 0.7s cubic-bezier(0.16, 1, 0.3, 1) 0.15s both;
}

@keyframes nc-browser-enter {
  from { opacity: 0; transform: translateY(16px) scale(0.97); }
  to { opacity: 1; transform: translateY(0) scale(1); }
}

.nc-browser-toolbar {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 10px 14px;
  background: rgba(255, 255, 255, 0.04);
  border-bottom: 1px solid rgba(255, 255, 255, 0.06);
  flex-shrink: 0;
}

.nc-browser-dots {
  display: flex;
  gap: 6px;
  flex-shrink: 0;
}

.nc-bdot {
  width: 10px;
  height: 10px;
  border-radius: 50%;
}
.nc-bdot-r { background: #ff5f57; }
.nc-bdot-y { background: #febc2e; }
.nc-bdot-g { background: #28c840; }

.nc-browser-url {
  flex: 1;
  display: flex;
  align-items: center;
  gap: 6px;
  padding: 4px 12px;
  background: rgba(0, 0, 0, 0.3);
  border-radius: 6px;
  font-size: 0.6rem;
  font-family: 'Inter', system-ui, sans-serif !important;
  color: rgba(255, 255, 255, 0.4);
  overflow: hidden;
  white-space: nowrap;
}

.nc-lock-icon {
  color: #4ade80;
  flex-shrink: 0;
}

.nc-browser-actions {
  display: flex;
  gap: 4px;
  flex-shrink: 0;
}

.nc-browser-btn {
  font-size: 0.7rem;
  width: 22px;
  height: 22px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 4px;
  color: rgba(255, 255, 255, 0.25);
}

.nc-browser-body {
  flex: 1;
  background: rgba(0, 0, 0, 0.2);
  padding: 1.5rem;
  overflow: auto;
  min-height: 0;
}
</style>
