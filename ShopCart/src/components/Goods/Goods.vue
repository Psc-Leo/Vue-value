<template>
  <div class="goods-container">
    <!-- 左侧图片 -->
    <div class="thumb">
      <div class="custom-control custom-checkbox">
        <!-- 复选框 -->
        <input type="checkbox" class="custom-control-input" :id="'cb' + id" :checked="state" @change="stateChange" />
        <label class="custom-control-label" for="'cb' + id">
          <!-- 商品的缩略图 -->
          <img :src="img" alt="" />
        </label>
      </div>
    </div>
    <!-- 右侧信息区域 -->
    <div class="goods-info">
      <!-- 商品标题 -->
      <h6 class="goods-title">{{ title }}</h6>
      <div class="goods-info-bottom">
        <!-- 商品价格 -->
        <span class="goods-price">￥ {{ price.toFixed(2) }}</span>
        <!-- 商品的数量 -->
        <!-- // s 兄弟间传值 -->
        <!-- <Counter :count="count" :id="id"></Counter> -->
        <!-- // s 插槽 -->
        <slot></slot>
      </div>
    </div>
  </div>
</template>

<script>
// s 兄弟间传值
// import Counter from '@/components/Counter/Counter.vue'

export default {
  props: {
    id: {
      type: Number,
      required: true
    },
    title: {
      type: String,
      default: ''
    },
    price: {
      type: Number,
      default: 0
    },
    img: {
      type: String,
      default: ''
    },
    state: {
      type: Boolean,
      default: true
    },
    count: {
      type: Number,
      default: 1
    }
  },
  // s 兄弟间传值
  /* components: {
    Counter
  }, */
  methods: {
    stateChange(e) {
      this.$emit('state-change', { id: this.id, value: e.target.checked })
    }
  }
}
</script>

<style lang="less" scoped>
.goods-container {
  + .goods-container {
    border-top: 1px solid #efefef;
  }
  padding: 10px;
  display: flex;
  .thumb {
    display: flex;
    align-items: center;
    img {
      width: 100px;
      height: 100px;
      margin: 0 10px;
    }
  }

  .goods-info {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    flex: 1;
    .goods-title {
      font-weight: bold;
      font-size: 12px;
    }
    .goods-info-bottom {
      display: flex;
      justify-content: space-between;
      .goods-price {
        font-weight: bold;
        color: red;
        font-size: 13px;
      }
    }
  }
}
</style>
