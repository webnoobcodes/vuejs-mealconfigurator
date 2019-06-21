<template>
  <transition-group class="progress-container" name="progress-in">
    <div class="progress-step"
    :class="{'active': index === activeConfigStep}"
    v-for="(option,index) in getConfiguration"
    :key="'step'+index"
    :style="{'--indexProgress': index}">
      {{ index +1 }}
    </div>
  </transition-group>
</template>

<script>
  export default {
    props: [
      'activeConfigStep',
      'configuration'
    ],
    data: () => {
      return {
        showProgress: false
      }
    },
    computed: {
      getConfiguration() {
        return this.showProgress === true ? this.configuration : [];
      }
    },
    mounted() {
      this.showProgress = true;
    }
  }
</script>

<style lang="scss" scoped>
  .progress-container {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    height: 50px;
    margin-bottom: 10px;
  }

  .progress-step {
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;
    width: 30px;
    height: 30px;
    border-radius: 50%;
    margin: 0 10px;
    color: #fff;
    background-color: #28a1ba;
    font-weight: bold;
    transition: all .8s ease-in-out;

    &.active {
      background-color: #28a1ba;

      ~ .progress-step {
        color: #555;
        background-color: #fff;
      }

      ~ .progress-step::before {
        background-color: #fff;
      }
    }

    &:before {
      content: '';
      position: absolute;
      left: -20px;
      width: 20px;
      height: 2px;
      background-color: #28a1ba;
      transition: all .4s ease-in-out;
      z-index: 10;
    }

    &:first-child::before {
      display: none;
    }
  }

  .progress-in-enter-active, .progress-in-leave-active {
    transition: opacity 1s linear;
    transition-delay: calc( .2s * var(--indexProgress));
  }

  .progress-in-enter, .progress-in-leave-to {
    opacity: 0;
  }
</style>
