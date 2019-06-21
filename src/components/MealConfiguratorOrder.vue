<template>
  <div class="order-container">
    <transition-group name="slide-in">
      <div class="order-position"
      :class="{'total':index === getConfiguration.length -1}"
      v-for="(position,index) in getConfiguration"
      :key="'pos'+index"
      :style="{'--indexOrder': index}">
        <img v-if="position.selectedOption.img" :src="require('../assets/icons/'+position.selectedOption.img)" alt="">
        <div class="title">{{ position.selectedOption.title }}</div>
        <div class="price">{{ position.selectedOption.price }} €</div>
      </div>
    </transition-group>
    <div class="actions">
      <button :class="{'show':showButton}">Order Now</button>
    </div>
  </div>
</template>

<script>
  export default {
    props: [
      'configuration'
    ],
    data: () => {
      return {
        showOrder: false,
        showButton: false
      }
    },
    computed: {
      getConfiguration() {
        return this.showOrder === true ? this.configuration : [];
      }
    },
    mounted() {
      this.showOrder = true;
      setTimeout(() => {
        this.showButton = true;
      }, 800);
    }
  }
</script>

<style lang="scss" scoped>
  .order-position {
    padding: 8px 20px 2px;
    width: calc(100% - 40px);
    height: 40px;
    border-top: 1px solid #ddd;

    img {
      float: left;
      width: 32px;
      height: auto;
      margin-right: 10px;
    }
    .title { float: left; padding-top: 8px; }
    .price { float: right; padding-top: 8px; }

    &.total {
      border-top: 1px solid #333;
      font-weight: bold;
      .title { padding-left: 42px; }
    }
  }

  .actions {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    height: 140px;
  }

  button {
    outline: none;
    border: none;
    color: #fff;
    background-color: #28a1ba;
    font-family: 'Ubuntu', Arial;
    font-size: 1.2rem;
    padding: 5px 20px;
    border-radius: 5px;
    cursor: pointer;
    opacity: 0;
    transition: opacity .5s ease-in-out;

    &.show {
      opacity: 1;
    }
  }

  .slide-in-enter-active {
    transition: opacity .2s linear, transform .5s cubic-bezier(.2,.5,.1,1);
    transition-delay: calc( .1s * var(--indexOrder));
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
