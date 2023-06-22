<template>
  <main class="main">
    <h1 v-if="!openPop">Essa aplicação é apenas para a demonstração do pop-up!</h1>
    <PopUp :openPop="openPop" :closePopUp="closePopUp" :openLeftPopUp="openLeftPopUp" />
    <LeftPopUp :openLeftPop="openLeftPop" :openPop="openPop" :closeLeftPop="closeLeftPop" />
  </main>
</template>

<script>
  import PopUp from '@/components/PopUp.vue';
  import LeftPopUp from '@/components/LeftPopUp.vue';

  export default {
    name: 'HomePage',
    components: {
      PopUp,
      LeftPopUp
    },
    data() {
      return {
        openPop: true,
        openLeftPop: false
      }
    },
    methods: {
      closePopUp() {
        this.openPop = false;
      },
      openLeftPopUp() {
        this.openLeftPop = true;
      },
      closeLeftPop() {
        this.openLeftPop = false;
      }
    }
  }
</script>

<style>
  @keyframes slideInFromLeft {
    0% {
      transform: translateX(-100%);
    }
    100% {
      transform: translateX(0);
    }
  }

  h1 {
    animation: 1s ease-out 0s 1 slideInFromLeft;
  }
</style>
