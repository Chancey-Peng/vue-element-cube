<template>
  <div class="cartcontrol">
    <transition name="move">
      <div class="cart-decrease" v-show="food.count>0" @click.stop.prevent="decreaseCart">
        <span class="inner icon-remove_circle_outline"></span>
      </div>
    </transition>
    <div class="cart-count" v-show="food.count>0">{{food.count}}</div>
    <div class="cart-add icon-add_circle" @click.stop.prevent="addCart"></div>
  </div>
</template>
<script>
import Vue from "vue";

const EVENT_ADD = "add";

export default {
  props: {
    food: {
      type: Object
    }
  },
  // created() {
  //   console.log(this.food);
  // },
  methods: {
    addCart(event) {
      // 防止pc端多次被点击
      if (!event._constructed) {
        return;
      }
      // console.log("click");
      if (!this.food.count) {
        // this.food.count = 1;
        // 通过vue属性，可以观测到count的变化
        // Vue.set(this.food, "count", 1);
        this.$set(this.food, "count", 1);
      } else {
        this.food.count++;
      }
      // 调用小球动画添加商品
      // this.$emit("cart.add", event.target);
      this.$emit(EVENT_ADD);
    },
    decreaseCart(event) {
      if (!event._constructed) {
        return;
      }
      if (this.food.count) {
        this.food.count--;
      }
    }
  }
};
</script>
<style lang="stylus" scoped>
.cartcontrol {
  font-size: 0px;

  .cart-decrease {
    display: inline-block;
    padding: 6px;
    opacity: 1;
    transform: translate3d(0, 0, 0);

    .inner {
      display: inline-block;
      line-height: 24px;
      font-size: 24px;
      color: rgb(0, 160, 220);
      transition: all 0.4s linear;
      transform: rotate(0);
    }

    // line-height: 24px;
    // font-size: 24px;
    // color: rgb(0, 160, 220);
    &.move-enter-active, &.move-leave-active {
      transition: all 0.4s linear;
    }

    &.move-enter, &.move-leave-active {
      opacity: 0;
      transform: translate3d(24px, 0, 0);

      .inner {
        transform: rotate(180deg);
      }
    }
  }

  .cart-count {
    display: inline-block;
    vertical-align: top;
    width: 12px;
    padding-top: 6px;
    line-height: 24px;
    text-align: center;
    font-size: 12px;
    color: rgb(147, 153, 159);
  }

  .cart-add {
    display: inline-block;
    padding: 6px;
    line-height: 24px;
    font-size: 24px;
    color: rgb(0, 160, 220);
  }
}
</style>
