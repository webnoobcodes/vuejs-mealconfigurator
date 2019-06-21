<template>
  <transition-group name="slide-in">
    <div class="option"
    v-for="(option,index) in getOptions"
    :key="'opt'+index"
    :style="{'--index': index}"
    @click="selectOption(option)">
      <img v-if="option.img" :src="require('../assets/icons/'+option.img)" alt="">
      <div class="title">{{ option.title }}</div>
      <div class="price">{{ option.price }} €</div>
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
        showOptions: false
      }
    },
    computed: {
      getOptions() {
        return this.showOptions === true ?
          this.configuration[this.activeConfigStep].options : [];
      }
    },
    methods: {
      selectOption(option) {
        this.showOptions = false;

        if(this.activeConfigStep +1 < this.configuration.length) {
          setTimeout(() => {
            this.$emit('chooseOption', option);
            this.showOptions = true;
          }, 500);
        }
      }
    },
    mounted() {
      this.showOptions = true;
    }
  }
</script>

<style lang="scss" scoped>
  .option {
    padding: 8px 20px 2px;
    width: calc(100% - 40px);
    height: 40px;
    border-top: 1px solid #ddd;
    cursor: pointer;

    img {
      float: left;
      width: 32px;
      height: auto;
      margin-right: 10px;
    }
    .title { float: left; padding-top: 8px; }
    .price { float: right; padding-top: 8px; }
  }

  .slide-in-enter-active {
    transition: opacity .2s linear, transform .5s cubic-bezier(.2,.5,.1,1);
    transition-delay: calc( .1s * var(--index));
  }

  .slide-in-leave-active {
    transition: opacity .5s linear;
  }

  .slide-in-enter {
    opacity: 0;
    transform: translateY(5em);
  }

  .slide-in-leave-to {
    opacity: 0;
  }
</style>
