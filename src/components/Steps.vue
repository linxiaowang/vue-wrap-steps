<template>
  <div class="v-steps" :class="{'step-center': stepLength < stepNumber}">
    <div
      v-for="(item, index) in data"
      :key="index"
      class="v-step"
      :style="handleStepStyle(index)"
      :class="getStatusClass(index)"
    >
      <div class="v-step-head">
        <div class="v-step-icon is-text">
          <i v-if="isSuccess(index)" class="el-icon-check" />
          <span v-else>{{ index + 1 }}</span>
        </div>
        <div v-show="straightLineDisplay(index)" class="v-step-line" />
        <div
          v-show="circleLineDisplay(index)"
          :class="getCircleClass(index)"
        />
      </div>
      <div class="v-step-main">
        <div class="v-step-title is-success">
          {{ item.title }}
        </div>
        <div class="v-step-description" :title="item.description">
          {{ item.description }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'VSteps',
  props: {
    active: {
      type: Number,
      default: 0
    },
    data: {
      type: Array,
      default: () => []
    },
    stepNumber: {
      type: Number,
      default: 5
    }
  },
  computed: {
    stepLength(){
      return this.data.length
    }
  },
  methods: {
    straightLineDisplay(index) {
      const actualIndex = index + 1
      if (actualIndex === this.data.length && actualIndex < this.stepNumber) {
        return false
      }
      if (actualIndex < this.stepNumber) {
        return true
      }
      // 奇数行最后一项
      if (actualIndex % this.stepNumber === 0 && (actualIndex / this.stepNumber) % 2 > 0) {
        return false
      }
      // 偶数反向行第一项
      if (actualIndex % this.stepNumber === 1 && Math.floor(actualIndex / this.stepNumber) % 2 > 0) {
        return false
      }
      // 最后一项且该行是正向
      if (
        Math.ceil(actualIndex / this.stepNumber) % 2 > 0
        && actualIndex === this.data.length
      ) {
        return false
      }
      return true
    },

    circleLineDisplay(index) {
      const actualIndex = index + 1
      if (actualIndex < this.stepNumber || actualIndex === this.data.length) {
        return false
      }
      // 整数倍
      if (actualIndex % this.stepNumber === 0) {
        return true
      }
      return false
    },

    getCircleClass(index) {
      const actualIndex = index + 1
      if (actualIndex % this.stepNumber === 0 && (actualIndex / this.stepNumber) % 2 > 0) {
        return 'right-circle'
      }
      return 'left-circle'
    },

    isSuccess(index) {
      const actualIndex = index + 1
      if (actualIndex < this.active) {
        return true
      }
      return false
    },

    getStatusClass(index) {
      const actualIndex = index + 1
      if (actualIndex < this.active) {
        return 'is-success'
      }
      if (actualIndex === this.active) {
        return 'is-process'
      }
      return 'is-wait'
    },

    handleStepStyle(index){
      const styleObj = {}
      if (Math.floor((index / this.stepNumber)) % 2 === 0){
        styleObj.order = index
      } else {
        styleObj.float = 'right'
      }

      if (index > this.stepNumber - 1){
        styleObj.marginTop = '23px'
      }
      styleObj.width = `${1 / this.stepNumber * 100}%`
      return styleObj
    }
  }
}
</script>

<style lang="scss" scoped>
.v-steps {
  overflow: hidden;
  width: 100%;

  .v-step {
    display: inline-flex;
    align-items: center;
    float: left;
    flex-direction: column;
    flex-grow: 1;

    &-head {
      position: relative;
      display: flex;
      justify-content: center;
      width: 100%;
    }

    &-line {
      position: absolute;
      top: 50%;
      right: -50%;
      left: 50%;
      width: 100%;
      height: 1px;
      background-color: $--color-text-placeholder;
    }

    &-icon {
      position: relative;
      z-index: 1;
      display: flex;
      justify-content: center;
      align-items: center;
      border: 1px solid $--color-text-placeholder;
      border-radius: 50%;
      width: 19px;
      height: 19px;
      font-size: 12px;

      // text-align: center;
      color: $--color-text-placeholder;
      background-color: #fff;

      &::before,
      &::after {
        content: "";
        position: absolute;
        display: inline-block;
        width: 8px;
        height: 100%;
        background-color: #fff;
      }

      &::before {
        left: -9px;
      }

      &::after {
        right: -9px;
      }
    }

    &-main {
      width: 100%;
    }

    &-title {
      // line-height: 38px;
      margin: 10px 0 3px;
      width: 100%;
      text-align: center;
    }

    &-description {
      overflow: hidden;
      width: 100%;
      font-size: 12px;
      text-align: center;
      text-overflow: ellipsis;
      white-space: nowrap;
      padding: 0 5px;
    }

    .right-circle {
      position: absolute;
      top: 10px;
      left: 48%;
      border: 1px solid $--color-text-placeholder;
      border-left: none;
      border-radius: 0 100% 100% 0 / 50%;
      width: 50%;
      height: 90px;
    }

    .left-circle {
      position: absolute;
      top: 10px;
      left: 5px;
      border: 1px solid $--color-text-placeholder;
      border-right: none;
      border-radius: 100% 0 0 100% / 50%;
      width: 50%;
      height: 85px;
    }
  }

  .is-success {
    .v-step-icon {
      border-color: $--color-primary;
      color: $--color-primary;
    }

    .v-step-line {
      background-color: $--color-primary;
    }
    .left-circle, .right-circle{
      border-color: $--color-primary;
    }
  }

  .is-process {
    .v-step-icon {
      border-color: $--color-primary;
      color: #fff;
      background-color: $--color-primary;
    }
  }

  .is-wait {
    .v-step-title {
      color: $--color-text-placeholder;
    }
  }
}

.step-center {
  display: flex;
  justify-content: center;
}
</style>
