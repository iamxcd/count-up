<template>
  <div ref="countto">
    <div class="dataNums in-row">
      <span v-for="(item,index) in valLen" :key="index" class="dataOne">
        <div class="box">
          <div ref="num_items" :style="ttClass" class="tt" t="38">
            <span :class="numStyle">0</span>
            <span :class="numStyle">1</span>
            <span :class="numStyle">2</span>
            <span :class="numStyle">3</span>
            <span :class="numStyle">4</span>
            <span :class="numStyle">5</span>
            <span :class="numStyle">6</span>
            <span :class="numStyle">7</span>
            <span :class="numStyle">8</span>
            <span :class="numStyle">9</span>
            <span :class="numStyle">0</span>
            <span :class="numStyle">1</span>
            <span :class="numStyle">2</span>
            <span :class="numStyle">3</span>
            <span :class="numStyle">4</span>
            <span :class="numStyle">5</span>
            <span :class="numStyle">6</span>
            <span :class="numStyle">7</span>
            <span :class="numStyle">8</span>
            <span :class="numStyle">9</span>
          </div>
          <span class="odometer_line" />
        </div>
      </span>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    num: {
      type: Number,
      required: true
    },
    options: {
      type: Object,
      default: () => {
        return {
          duration: 2, // 动画时间
          transitionTiming: "ease",
          digit: 0 // 默认显示几位数
        };
      }
    }
  },
  data() {
    return {
      ttClass: {}
    };
  },
  computed: {
    valLen() {
      return this.options.digit || (this.num + "").length;
    },
    numStyle() {
      return {};
    }
  },
  watch: {
    num() {
      this.scroNum();
    }
  },
  mounted() {
    this.scroNum();
  },
  methods: {
    scroNum() {
      var number = this.num;
      var $num_item = this.$refs.num_items;
      var h = $num_item[0].offsetHeight;
      // 组装 动画样式
      this.ttClass = {
        transition: `all ${this.options.duration + "s"} ${
          this.options.transitionTiming
        }`
      };
      var numberStr = number.toString();
      if (numberStr.length <= $num_item.length - 1) {
        var tempStr = "";
        for (var a = 0; a < $num_item.length - numberStr.length; a++) {
          tempStr += "0";
        }
        numberStr = tempStr + numberStr;
      }

      var numberArr = numberStr.split("");

      $num_item.forEach(function(item, i) {
        setTimeout(function() {
          const top = -parseInt(numberArr[i]) * h - h * 10 + "px";
          item.style.top = top;
        }, i * 10); // 每个牌子 转动间隔时间
      });
    }
  }
};
</script>

<style scoped>
.in-row {
  font-family: arial;
}
.in-row > li,
.in-row span {
  display: inline-block;
  font-size: 14px;
  letter-spacing: normal;
  word-spacing: normal;
}
.dataNums {
  display: inline-block;
}
.dataNums .dataOne {
  width: 15px;
  height: 30px;
  margin: 0;
  text-align: center;
  border: 1px solid red;
  padding: 1px;
  margin: 0 1px 0 1px;
  border-radius: 5px;
}
.dataNums .box {
  position: relative;
  width: 100%;
  height: 100%;
  overflow: hidden;
}
.dataNums .box .tt {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}
.dataNums .tt span {
  width: 100%;
  height: 100%;
  font: bold 30px "Arial";
  color: red;
}
.odometer_line {
  position: absolute;
  z-index: 3;
  display: inline-block;
  width: 100%;
  height: 1px;
  background-color: #aaa;
  opacity: 0.6;
  top: 50%;
  left: 0px;
}
</style>
