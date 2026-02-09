<!--
  NcKbd — Styled keyboard shortcut display.
  
  Usage:
    Press <NcKbd>⌘</NcKbd> + <NcKbd>K</NcKbd> to search
-->
<template>
  <kbd class="nc-kbd"><slot /></kbd>
</template>

<style scoped>
.nc-kbd {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  min-width: 22px;
  height: 22px;
  padding: 0 6px;
  font-size: 0.6rem;
  font-weight: 700;
  font-family: 'Inter', system-ui, sans-serif !important;
  color: rgba(255, 255, 255, 0.7);
  background: linear-gradient(180deg, rgba(255, 255, 255, 0.08) 0%, rgba(255, 255, 255, 0.03) 100%);
  border: 1px solid rgba(255, 255, 255, 0.12);
  border-bottom-width: 2px;
  border-radius: 6px;
  box-shadow:
    0 1px 3px rgba(0, 0, 0, 0.3),
    inset 0 1px 0 rgba(255, 255, 255, 0.06);
  vertical-align: middle;
  line-height: 1;
}
</style>
