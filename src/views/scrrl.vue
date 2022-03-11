<template>
  <div class="wrap">
    <div id="box">
      <div id="marquee">{{ text }}</div>
      //展示的文字
      <div id="copy"></div>
    </div>
    <div id="node">{{ text }}</div>
  </div>
</template>
<script lang="ts">
export default {
  name: 'Marquee',
  props: ['lists'], // 父组件传入数据， 数组形式 [ "连雨不知春去"，"一晴方觉夏深"]
  data() {
    return {
      text: '' // 数组文字转化后的字符串
    };
  },
  methods: {
    move() {
      // 获取文字text 的计算后宽度  （由于overflow的存在，直接获取不到，需要独立的node计算）
      let width = document.getElementById('node').getBoundingClientRect().width;
      let box = document.getElementById('box');
      let copy = document.getElementById('copy');
      copy.innerText = this.text; // 文字副本填充
      let distance = 0; // 位移距离
      //设置位移
      setInterval(function () {
        distance = distance - 1;
        // 如果位移超过文字宽度，则回到起点
        if (-distance >= width) {
          distance = 16;
        }
        box.style.transform = 'translateX(' + distance + 'px)';
      }, 20);
    }
  },
  // 把父组件传入的arr转化成字符串
  mounted: function () {
    for (let i = 0; i < this.lists.length; i++) {
      this.text += ' ' + this.lists[i];
    }
  },
  // 更新的时候运动
  updated: function () {
    let times: number;
    times = setTimeout(() => {
      let wrapw = document.getElementById('wrap').offsetWidth;
      let nodew = document.getElementById('node').offsetWidth;
      if (wrapw < nodew) {
        //判断文字长度大于盒子宽度时，执行滚动
        this.move();
      }
      clearTimeout('times');
    }, 2000);
  }
};
</script>
<style scoped>
.wrap {
  overflow: hidden;
  height: 30px;
  line-height: 30px;
}

#box {
  width: 80000%;
}

#box div {
  float: left;
}

#marquee {
  margin: 0 16px 0 0;
}

#node {
  position: absolute;
  z-index: -999;
  top: -999999px;
}
</style>
