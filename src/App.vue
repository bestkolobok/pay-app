<template>
  <v-app id="main-app">
    <app-header class="header"></app-header>
    <v-content class="content-conteiner"> 
      <app-strings></app-strings>
      <app-buttons></app-buttons>
    </v-content>
    <app-footer class="footer"></app-footer>
  </v-app>
</template>

<script>
import AppHeader from '@/components/Header.vue'
import AppFooter from '@/components/Footer.vue'
import AppStrings from '@/components/StringsBar.vue'
import AppButtons from '@/components/Buttons.vue'
export default {
  name: 'App',
  components: { AppHeader, AppFooter, AppButtons, AppStrings },
}
</script>

<style lang="scss" scoped>

</style>
