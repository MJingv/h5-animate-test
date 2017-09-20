<template>
<div>


  <div class="hello" ref='wrap'>
    <canvas ref="canvas" id="canvas" width="800" height="800" style="border:1px solid #ccc"></canvas>
    <!--
  <div class="item one"><img src="../assets/l1.png"></div>
  <div class="item two "><img src="../assets/l2.png"></div>
  <div class="item three"><img src="../assets/l3.png"></div> -->


  </div>

  <button @click='prev' type="button" name="button">上一张</button>
  <button type="button" name="button">下一张</button>
</div>
</template>

<script>
import 'yuki-createjs'
var async = require('async');

export default {

  name: 'hello',
  data() {
    return {
      canvas: '',
      ctx: '',
  
      tangramArr: [{
          coordinateArr: [{
            x: 0,
            y: 0
          }, {
            x: 800,
            y: 0
          }, {
            x: 400,
            y: 400
          }],
          color: '#caff67'
        },
        {
          coordinateArr: [{
            x: 0,
            y: 0
          }, {
            x: 400,
            y: 400
          }, {
            x: 0,
            y: 800
          }],
          color: '#67becf'
        },
        {
          coordinateArr: [{
            x: 800,
            y: 0
          }, {
            x: 800,
            y: 400
          }, {
            x: 600,
            y: 600
          }, {
            x: 600,
            y: 200
          }],
          color: '#ef3d61'
        },
        {
          coordinateArr: [{
            x: 600,
            y: 200
          }, {
            x: 600,
            y: 600
          }, {
            x: 400,
            y: 400
          }],
          color: '#f9f51a'
        },
        {
          coordinateArr: [{
            x: 400,
            y: 400
          }, {
            x: 600,
            y: 600
          }, {
            x: 400,
            y: 800
          }, {
            x: 200,
            y: 600
          }],
          color: '#a594c0'
        },
        {
          coordinateArr: [{
            x: 200,
            y: 600
          }, {
            x: 400,
            y: 800
          }, {
            x: 0,
            y: 800
          }],
          color: '#fa8ecc'
        },
        {
          coordinateArr: [{
            x: 800,
            y: 400
          }, {
            x: 800,
            y: 800
          }, {
            x: 400,
            y: 800
          }],
          color: '#caff67'
        },
      ]
    }
  },
  methods: {
    prev() {
      this.left = this.left -300
      console.log(this.left);

    },
    draw(item) {
      var coordinateArr = item.coordinateArr
      var color = item.color
      this.ctx.beginPath();
      this.ctx.moveTo(coordinateArr[0].x, coordinateArr[0].y)
      coordinateArr.map((i) => {
        this.ctx.lineTo(i.x, i.y)
      })
      this.ctx.closePath()

      this.ctx.fillStyle = color
      this.ctx.fill();
    },
    sleep(ms) {
      return new Promise(function(resolve, reject) {
        setTimeout(resolve, ms);
      });
    },
    async asyncDraw() {
      // await this.sleep(1000)
      // this.tangramArr.map((item) => {
      //   return this.draw(item)
      // });
      //for循环方法
      for (let i = 0; i < this.tangramArr.length; i++) {
        await this.sleep(1000);
        this.draw(this.tangramArr[i]);
      };




      //递归方法
      // const item = this.tangramArr.shift();
      // await this.sleep(1000);
      // this.draw(item);
      // if (this.tangramArr.length > 0) {
      //   // debugger;
      //   this.asyncDraw();
      // }
    },
    begin() {
      this.asyncDraw()

      //二分查找
      // var res = this.div(3, [1, 2, 3, 4, 5])
      // console.log(res);

    },
    quickSort(arr, low, high) {
      var mid = this.partiton(arr, low, high)
      this.quickSort(arr, low, mid - 1)
      this.quickSort(arr, mid + 1, high)

    },
    partiton(arr, low, high) {
      var pivot = arr[low]
      while (pivot >= arr[low]) {
        low++
      }
      arr[low] = arr[high]
      while (pivot <= arr[high]) {
        high++
      }
      arr[high] = arr[low]
      arr[low] = pivot
      return low
    },
    div(x, arr, low = 0, high = arr.length - 1) {
      //二分查找

      //递归解法
      // const mid = parseInt(low+high)/2
      // if(x<arr[mid]){
      //     this.div(x,arr,low,mid-1)
      // }else if(x>arr[mid]){
      //     this.div(x,arr,mid+1,high)
      // }else if (x==arr[mid]) {
      //   return `[${mid}]-${arr[mid]}`
      // }

      //非递归
      // const mid = parseInt((low+high)/2)
      // while(low< high){
      //   if(x<arr[mid]){
      //     high = mid -1
      //   }else if (x>arr[mid]) {
      //     low=mid+1
      //   }else {
      //     return `[${mid}]-${arr[mid]}`
      //   }
      // }

    }

  },

  mounted() {

    this.canvas = this.$refs.canvas
    this.ctx = canvas.getContext('2d')
    this.begin()

  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped scoped lang="stylus" rel="stylesheet/stylus">
.scroll
  border: 3px solid #ccc
  img
    width: 200px;
    height: 200px;
.hello
  display: flex
 .one
   animation:1s one  infinite alternate-reverse
 .two
    transform-origin:0 0
    animation:1s two  infinite alternate-reverse
 .three
    animation:5s  three  infinite

    @keyframes two
      from
        transform:rotate(0deg)  translateX(0)
      to
         transform:rotate(5deg) translateX(30px)

    @keyframes one
      from
        transform: none
        opacity:0
      to
        transform: scale(1.2)
        opacity:1
    @keyframes three
          from
            transform:  translateY(100%)
          to
             transform: translateY(-100%)





</style>
