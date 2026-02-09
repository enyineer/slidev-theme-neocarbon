<!--
  NeοCarbon — Intro / About Me Layout
  Speaker introduction slide with a large avatar area and bio content.

  Usage:
    ---
    layout: intro
    ---
    # Jane Doe
    **Lead Engineer** at Acme Corp

    - 10+ years software architecture
    - AI & ML specialist
    - Open source contributor
-->
<template>
  <div class="slidev-layout nc-intro nc-custom-layout">
    <div class="nc-intro-accent" />
    <div class="nc-intro-inner">
      <slot />
    </div>
  </div>
</template>

<style scoped>
.nc-intro {
  display: flex !important;
  flex-direction: row !important;
  align-items: center !important;
  height: 100%;
  padding: 2.5rem 3rem !important;
  position: relative;
  overflow: hidden;
}

/* Side accent bar */
.nc-intro-accent {
  position: absolute;
  left: 0;
  top: 10%;
  bottom: 10%;
  width: 4px;
  background: linear-gradient(
    180deg,
    transparent,
    var(--nc-accent) 30%,
    var(--nc-accent) 70%,
    transparent
  );
  border-radius: 0 4px 4px 0;
  box-shadow: 0 0 20px rgba(var(--nc-accent-rgb, 227, 6, 19), 0.4);
  animation: nc-accent-bar 1s cubic-bezier(0.16, 1, 0.3, 1) 0.1s both;
}

@keyframes nc-accent-bar {
  from {
    opacity: 0;
    transform: scaleY(0);
  }
  to {
    opacity: 1;
    transform: scaleY(1);
  }
}

.nc-intro-inner {
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding-left: 1.5rem;
  animation: nc-intro-enter 0.7s cubic-bezier(0.16, 1, 0.3, 1) 0.2s both;
}

@keyframes nc-intro-enter {
  from { opacity: 0; transform: translateX(20px); filter: blur(4px); }
  to { opacity: 1; transform: translateX(0); filter: blur(0); }
}

.nc-intro-inner :deep(h1) {
  font-size: 2.2rem !important;
  font-weight: 700 !important;
  letter-spacing: -0.02em;
  margin-bottom: 0.25rem !important;
}

.nc-intro-inner :deep(p) {
  color: var(--nc-text-muted) !important;
  font-size: 0.85rem !important;
  line-height: 1.6;
}

.nc-intro-inner :deep(strong) {
  color: var(--nc-accent) !important;
}

.nc-intro-inner :deep(ul) {
  margin-top: 1rem;
  list-style: none;
  padding: 0;
}

.nc-intro-inner :deep(li) {
  font-size: 0.78rem !important;
  color: var(--nc-text-muted) !important;
  padding: 0.3rem 0;
  padding-left: 1.2rem;
  position: relative;
}

.nc-intro-inner :deep(li)::before {
  content: '';
  position: absolute;
  left: 0;
  top: 50%;
  transform: translateY(-50%);
  width: 6px;
  height: 6px;
  border-radius: 50%;
  background: var(--nc-accent);
  box-shadow: 0 0 8px rgba(var(--nc-accent-rgb, 227, 6, 19), 0.5);
}

.nc-intro-inner :deep(img) {
  width: 100px;
  height: 100px;
  border-radius: 50%;
  object-fit: cover;
  border: 2px solid rgba(var(--nc-accent-rgb, 227, 6, 19), 0.3);
  box-shadow: 0 0 30px rgba(var(--nc-accent-rgb, 227, 6, 19), 0.15);
  margin-bottom: 1rem;
}
</style>
