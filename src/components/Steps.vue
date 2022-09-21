<template>
  <div class="v-steps">
    <div
      v-for="(item, index) in data"
      :key="index"
      class="v-step"
      :class="getStatusClass(index)"
    >
      <div class="v-step-head">
        <div class="v-step-icon is-text">
          <i v-if="isSuccess(index)" class="el-icon-check"></i>
          <span v-else>{{ index + 1 }}</span>
        </div>
        <div v-show="straightLineDisplay(index)" class="v-step-line"></div>
        <div
          v-show="circleLineDisplay(index)"
          :class="getCircleClass(index)"
        ></div>
      </div>
      <div class="v-step-main">
        <div class="v-step-title is-success">12321</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'vSteps',
  props: {
    active: {
      type: Number,
      default: 5
    },
    data: {
      type: Array,
      default: () => [
        {
          title: '213',
          description: '12312'
        },
        {
          title: '213',
          description: '12312'
        },
        {
          title: '213',
          description: '12312'
        },
        {
          title: '213',
          description: '12312'
        },
        {
          title: '213',
          description: '12312'
        },
        {
          title: '213',
          description: '12312'
        },
        {
          title: '213',
          description: '12312'
        },
        {
          title: '213',
          description: '12312'
        },
        {
          title: '213',
          description: '12312'
        },
        {
          title: '213',
          description: '12312'
        },
        {
          title: '213',
          description: '12312'
        },
        {
          title: '213',
          description: '12312'
        },
        {
          title: '213',
          description: '12312'
        },
        {
          title: '213',
          description: '12312'
        },
        {
          title: '213',
          description: '12312'
        },
        {
          title: '213',
          description: '12312'
        },
        {
          title: '213',
          description: '12312'
        },
        {
          title: '213',
          description: '12312'
        },
        {
          title: '213',
          description: '12312'
        },
        {
          title: '213',
          description: '12312'
        },
        {
          title: '213',
          description: '12312'
        },
        {
          title: '213',
          description: '12312'
        },
        {
          title: '213',
          description: '12312'
        },
        {
          title: '213',
          description: '12312'
        },
        {
          title: '213',
          description: '12312'
        },
        {
          title: '213',
          description: '12312'
        },
        {
          title: '213',
          description: '12312'
        },
        {
          title: '213',
          description: '12312'
        },
        {
          title: '213',
          description: '12312'
        },
        {
          title: '213',
          description: '12312'
        },
      ]
    }
  },
  methods: {
    straightLineDisplay(index) {
      const actualIndex = index + 1;
      if (actualIndex === this.data.length && actualIndex < 6){
        return false
      }
      if (actualIndex < 6) {
        return true;
      }
      // 奇数行最后一项
      if (actualIndex % 6 === 0 && (actualIndex / 6) % 2 > 0) {
        return false;
      }
      // 偶数反向行第一项
      if (actualIndex % 6 === 1 && Math.floor(actualIndex / 6) % 2 > 0) {
        return false;
      }
      // 最后一项且该行是正向
      if (Math.ceil(actualIndex / 6) % 2 > 0 && actualIndex === this.data.length){
        return false
      }
      return true;
      // return actualIndex < 5 || actualIndex % 6 !== 0
    },

    circleLineDisplay(index) {
      const actualIndex = index + 1;
      if (actualIndex < 6 || actualIndex === this.data.length) {
        return false;
      }
      // 整数倍
      if (actualIndex % 6 === 0) {
        return true;
      }
      return false;
    },

    getCircleClass(index) {
      const actualIndex = index + 1;
      if (actualIndex % 6 === 0 && (actualIndex / 6) % 2 > 0) {
        return 'right-circle';
      }
      return 'left-circle';
    },

    isSuccess(index) {
      const actualIndex = index + 1;
      if (actualIndex < this.active) {
        return true;
      }
      return false;
    },

    getStatusClass(index) {
      const actualIndex = index + 1;
      if (actualIndex < this.active) {
        return 'is-success';
      }
      if (actualIndex === this.active) {
        return 'is-process';
      }
      return 'is-wait';
    }
  }
};
</script>

<style lang="scss" scoped>
.v-steps {
  width: 520px;
  margin-top: 50px;
  .v-step {
    display: inline-flex;
    flex-direction: column;
    align-items: center;
    width: 16.66%;
    flex-grow: 1;
    float: left;

    @for $i from 0 through 150 {
      &:nth-child(#{$i + 1}) {
        @if floor($i / 6) % 2 == 0 {
          order: #{$i};
        } @else {
          // order: #{$i + (2 - ($i % 6)) * 2};
          float: right;
        }
      }
    }

    &-head {
      position: relative;
      display: flex;
      justify-content: center;
      width: 100%;
    }

    &-line {
      position: absolute;
      top: 50%;
      left: 50%;
      right: -50%;
      width: 100%;
      height: 1px;
      background-color: #c6cacd;
    }

    &-icon {
      position: relative;
      display: flex;
      align-items: center;
      justify-content: center;
      width: 19px;
      height: 19px;
      font-size: 12px;
      // text-align: center;
      color: #c6cacd;
      border: 1px solid #c6cacd;
      border-radius: 50%;
      z-index: 1;
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

    &-title {
      line-height: 38px;
    }

    .right-circle {
      position: absolute;
      top: 10px;
      left: 50%;
      width: 50px;
      height: 80px;
      border: 1px solid #c6cacd;
      border-radius: 0 100% 100% 0/50%;
      border-left: none;
    }

    .left-circle {
      position: absolute;
      top: 10px;
      left: -20%;
      width: 50px;
      height: 80px;
      border: 1px solid #c6cacd;
      border-radius: 100% 0 0 100%/50%;
      border-right: none;
    }

    &:nth-child(n + 7) {
      margin-top: 23px;
    }
  }

  .is-success {
    .v-step-icon {
      color: $primary-color;
      border-color: $primary-color;
    }
    .v-step-line{
      background-color: $primary-color;
    }
  }

  .is-process {
    .v-step-icon {
      color: #fff;
      background-color: $primary-color;
      border-color: $primary-color;
    }
  }

  .is-wait {
    .v-step-title{
      color: #c6cacd;
    }
  }
}
</style>
