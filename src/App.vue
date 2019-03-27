<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <div ref="chart"></div>
    <div class="canvas"  :style="{ 'background-image': 'url(' + blah + ')' }" ref="my-node">
      <h1>{{ message }}</h1>
      <div class="frame">
        <form id="form1" runat="server">
          <div class="demo"></div>
          <!-- <img id="blah" :src="blah" alt="your image"/> -->
        </form>
      </div>
    </div>
    <input type='file' id="imgInp" ref="image" @change="imgHandler" />
    <button class="download-btn" @click="recordImage">點我下載</button>
    <input type="text" name="message" v-model="message">
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import domtoimage from 'dom-to-image';
import FileSaver from 'file-saver'

var Highcharts = require('highcharts');

// Load module after Highcharts is loaded
require('highcharts/modules/exporting')(Highcharts);
// require('highcharts/modules/export-data')(Highcharts);


export default {
  name: 'app',
  data () {
    return {
      imgURL: '',
      blah: '',
      message: '請輸入你想要的話',
      // pigInfo: {
      //   credits: {
      //     enabled: false
      //   },
      //   chart: {
      //     zoomType: 'xy'
      //   },
      //   title: {
      //     text: '台灣豬肉出口產值'
      //   },
      //   subtitle: {
      //     text: '來源: 農委會'
      //   },
      //   xAxis: [{
      //     categories: ['78', '79', '80', '81', '82', '83',
      //       '84', '85', '86', '87', '88'],
      //     crosshair: true
      //   }],
      //   yAxis: [{ // Primary yAxis
      //     labels: {
      //       format: '{value} 噸',
      //       style: {
      //         color: Highcharts.getOptions().colors[1]
      //       },
      //       staggerLines: 100
      //     },
      //     title: {
      //       text: '重量（噸）',
      //       style: {
      //         color: Highcharts.getOptions().colors[1]
      //       }
      //     },
      //   }, { // Secondary yAxis
      //     title: {
      //       text: '產值（千美金）',
      //       style: {
      //         color: Highcharts.getOptions().colors[0]
      //       }
      //     },
      //     labels: {
      //       format: '{value} 千美金',
      //       style: {
      //         color: Highcharts.getOptions().colors[0]
      //       }
      //     },
      //     opposite: true
      //   }],
      //   tooltip: {
      //     shared: true
      //   },
      //   legend: {
      //     layout: 'vertical',
      //     align: 'left',
      //     x: 120,
      //     verticalAlign: 'top',
      //     y: 100,
      //     floating: true,
      //     backgroundColor: (Highcharts.theme && Highcharts.theme.legendBackgroundColor) || 'rgba(255,255,255,0.25)'
      //   },
      //   series: [{
      //     name: '重量',
      //     type: 'column',
      //     yAxis: 1,
      //     data: [113226, 158184, 228458, 215007, 198412, 233559, 268610, 274171, 49760, 1453, 219, 468, 1233, 1804, 1325, 1425, 1143, 1062, 1631, 2188, 1871, 1772, 2867, 2647, 2114, 1843, 1520, 1648, 1522, 1661],
      //     animation: {
      //         duration: 1500,
      //         easing: easeOutBounce
      //         // Uses simple function
      //     },
      //     tooltip: {
      //       valueSuffix: '噸'
      //     }
      //   }, {
      //     name: '產值',
      //     type: 'spline',
      //     data: [512525, 665896, 911054, 1023711, 1067568, 1207530, 1583484, 1568907, 243000, 2079, 948, 2978, 7316, 9726, 7114, 8403, 7309, 5889, 6985, 9539, 10371, 10333, 15597, 15186, 14829, 14059, 9894, 11351, 10928, 12388],
      //     animation: {
      //         duration: 2000
      //         // Uses simple function
      //     },
      //     tooltip: {
      //       valueSuffix: '千美金'
      //     }
      //   }]
      // },
      pigInfo2: {
        chart: {
          type: 'column',
          styledMode: true
        },

        title: {
          text: '台灣豬肉出口產值'
        },
        xAxis: [{
          categories: ['78', '79', '80', '81', '82', '83', '84', '85', '86', '87', '88', '89', '90', '91', '92', '93', '94', '95', '96', '97', '98', '99', '100', '101', '102', '103', '104', '105', '106', '107'],
          crosshair: true,
          title: {
            text: '年份（民國）'
          }
        }],
        yAxis: [{
          className: 'highcharts-color-0',
          title: {
            text: '重量（噸）'
          }
        }, {
          className: 'highcharts-color-1',
          opposite: true,
          title: {
            text: '產值（千美金）'
          }
        }],

        plotOptions: {
          column: {
            borderRadius: 5
          }
        },

        series: [{
          name: '重量（噸）',
          data: [113226, 158184, 228458, 215007, 198412, 233559, 268610, 274171, 49760, 1453, 219, 468, 1233, 1804, 1325, 1425, 1143, 1062, 1631, 2188, 1871, 1772, 2867, 2647, 2114, 1843, 1520, 1648, 1522, 1661],
          animation: {
              duration: 2000
              // Uses simple function
          }
        }, {
          name: '產值（千美金）',
          data: [512525, 665896, 911054, 1023711, 1067568, 1207530, 1583484, 1568907, 243000, 2079, 948, 2978, 7316, 9726, 7114, 8403, 7309, 5889, 6985, 9539, 10371, 10333, 15597, 15186, 14829, 14059, 9894, 11351, 10928, 12388],
          animation: {
              duration: 2000
              // Uses simple function
          },
          yAxis: 1
        }]

      }
    }
  },
  components: {
    HelloWorld
  },
  mounted () {
  
    var easeOutBounce = function (pos) {
        if ((pos) < (1 / 2.75)) {
            return (7.5625 * pos * pos);
        }
        if (pos < (2 / 2.75)) {
            return (7.5625 * (pos -= (1.5 / 2.75)) * pos + 0.75);
        }
        if (pos < (2.5 / 2.75)) {
            return (7.5625 * (pos -= (2.25 / 2.75)) * pos + 0.9375);
        }
        return (7.5625 * (pos -= (2.625 / 2.75)) * pos + 0.984375);
    };

    Math.easeOutBounce = easeOutBounce;

    let vm  = this
    let conf = {  }
    Highcharts.chart(vm.$refs['chart'], this.pigInfo2)
  console.log(Highcharts)
  },
  methods: {
    imgHandler () {
      this.readURL(this.$refs['image']);
    },
    readURL(input) {
      let vm = this
      if (input.files && input.files[0]) {
        var reader = new FileReader();

        reader.onload = function(e) {
          vm.blah = e.target.result
        }

        reader.readAsDataURL(input.files[0]);
      }
    },
    handleCanvas () {
      var canvas = this.$refs['canvas']
      var ctx = canvas.getContext("2d");
      

      // ctx.fillStyle = "green"
      // ctx.fillRect(10, 10, 100, 100)
      this.handleDrawImg(ctx)
      
    },
    handleDrawImg (pen) {
      var img = new Image();
      img.onload = function(){
        pen.drawImage(img,0,0, 100, 50);
        // pen.beginPath();
        // pen.moveTo(30,96);
        // pen.lineTo(70,66);
        // pen.lineTo(103,76);
        // pen.lineTo(170,15);
        // pen.stroke();
      };
      img.src = require('../public/image/getImage.jpg');
    },
    recordImage () {
      
      domtoimage.toBlob(this.$refs['my-node'])
        .then(function (blob) {
            FileSaver.saveAs(blob, 'my-node.png');
        });
    }
  },
  computed: {
    easeOutBounce: function (pos) {
        if ((pos) < (1 / 2.75)) {
            return (7.5625 * pos * pos);
        }
        if (pos < (2 / 2.75)) {
            return (7.5625 * (pos -= (1.5 / 2.75)) * pos + 0.75);
        }
        if (pos < (2.5 / 2.75)) {
            return (7.5625 * (pos -= (2.25 / 2.75)) * pos + 0.9375);
        }
        return (7.5625 * (pos -= (2.625 / 2.75)) * pos + 0.984375);
    }
  }
}
</script>
<style lang="scss">
@import './assets/CSS/highchart.css';

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  #container {
  height: 400px;
  max-width: 800px;
  margin: 0 auto;
}
  .canvas {
    width: 500px;
    height: 500px;
    border: solid 1px blue;
    position: relative;
    background-repeat: no-repeat;
    background-position: -100px -100px;
    h1 {
      position: relative;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      color: white;
    }
    .demo {
      
    }
  }
/* Link the series colors to axis colors */
  .highcharts-color-0 {
    fill: rgb(253, 215, 228);
    stroke: rgb(253, 215, 228);
  }
  .highcharts-axis.highcharts-color-0 .highcharts-axis-line {
    stroke: rgb(253, 215, 228);
  }
  .highcharts-axis.highcharts-color-0 text {
    fill: rgb(253, 215, 228);;
  }
  .highcharts-color-1 {
    fill: #85bb65;
    stroke: #85bb65;
  }
  .highcharts-axis.highcharts-color-1 .highcharts-axis-line {
    stroke: #85bb65;
  }
  .highcharts-axis.highcharts-color-1 text {
    fill: #85bb65;
  }


  .highcharts-yaxis .highcharts-axis-line {
    stroke-width: 2px;
  }
  .download-btn {
    width: 80px;
    height: 30px;
    border: 0px;
    background-color: pink;
    border-radius: 5px;
  }
}
</style>
