<template>
  <div>
    <app-header></app-header>
    <Nuxt />
    <app-footer></app-footer>
  </div>
</template>
<script>
import AppHeader from "@/components/main-style/AppHeader";
import AppFooter from "@/components/main-style/AppFooter";
export default {
  components: {
    AppHeader,
    AppFooter
  }
}
</script>
<style>
*,
*::before,
*::after {
  box-sizing: border-box;
  margin: 0;
}
</style>
