<template>
  <div id="app">
    <ApartmentsCatalog />
  </div>
</template>

<script>
import ApartmentsCatalog from './components/ApartmentsCatalog.vue'

export default {
  name: 'App',
  components: {
    ApartmentsCatalog
  }
}
</script>

<style lang="scss">
@font-face {
  font-family: 'TT Norms Pro';
  src: local('TT Norms Pro Bold'), local('TT-Norms-Pro-Bold'),
      url('~@/assets/fonts/TTNormsPro-Bold.woff2') format('woff2'),
      url('~@/assets/fonts/TTNormsPro-Bold.woff') format('woff'),
      url('~@/assets/fonts/TTNormsPro-Bold.ttf') format('truetype');
  font-weight: 700;
  font-style: normal;
}
@font-face {
  font-family: 'TT Norms Pro';
  src: local('TT Norms Pro Medium'), local('TT-Norms-Pro-Medium'),
      url('~@/assets/fonts/TTNormsPro-Medium.woff2') format('woff2'),
      url('~@/assets/fonts/TTNormsPro-Medium.woff') format('woff'),
      url('~@/assets/fonts/TTNormsPro-Medium.ttf') format('truetype');
  font-weight: 500;
  font-style: normal;
}
@font-face {
  font-family: 'TT Norms Pro';
  src: local('TT Norms Pro Regular'), local('TT-Norms-Pro-Regular'),
      url('~@/assets/fonts/TTNormsPro-Regular.woff2') format('woff2'),
      url('~@/assets/fonts/TTNormsPro-Regular.woff') format('woff'),
      url('~@/assets/fonts/TTNormsPro-Regular.ttf') format('truetype');
  font-weight: 400;
  font-style: normal;
}

body {
  background-color: #f8f8f8;
}

#app {
  font-family: "TT Norms Pro", Helvetica, Arial;
  max-width: 1000px;
  margin: 80px auto;
  color: #1f1f25;
}

h1 {
  font-size: 34px;
  margin: 0 0 32px;
}

h2 {
  margin: 0 0 24px;
}

button {
  font-family: "TT Norms Pro", Helvetica, Arial;
  color: #1f1f25;
  font-size: 16px;
  font-weight: 700;
  padding: 11px 60px;
  height: 40px;
  border: none;
  border-radius: 8px;
  cursor: pointer;

  &.primary {
    background-color: #ffd400;
    &:hover {
      background-color: #fdca21;
    }
    &:active {
      background-color: #ffd138;
    }
  }
  &.primary:disabled {
    background-color: #ffd400;
    cursor: default;
  }
  &.secondary {
    background-color: #f1f5f9;
    &:hover {
      background-color: #e5eff9;
    }
    &:active {
      background-color: #eaf1f9;
    }
  }
  &.secondary:disabled {
    background-color: #f1f5f9;
    cursor: default;
  }

  &:disabled {
    opacity: 0.5;
  }
}
</style>
