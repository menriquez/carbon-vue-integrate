<script>
import TutorialHeader from './components/TutorialHeader';

export default {
  name: 'App',
  components: {
    TutorialHeader
  }
};
</script>

<style lang="scss">
@import './styles/carbon';
</style>
<template>
  <div id="app">
    <tutorial-header />
    <cv-content id="#main-content">
      <!-- <cv-button>Button</cv-button> -->
      <router-view />
    </cv-content>
  </div>
</template>