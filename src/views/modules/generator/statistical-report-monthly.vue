<template>
  <div class="Echarts">
    <el-tabs tab-position="left" >
      <el-tab-pane label="员工班次情况">
        <div id="radarChart" style="width: 1000px;height: 600px;"></div>
        <p style="text-align: center">从图中可以看出整体的28天出勤员工班次数量极值差是较小的，200名员工班次数量均在16-22范围之间</p>
      </el-tab-pane>
      <el-tab-pane label="白夜班出勤人数分析">
        <div id="barChart" style="width: 1000px;height: 600px;"></div>
        <p style="text-align: center">从图中可以明显得知白夜班人数安排比例基本为1:1，较为符合当代大多数仓库实际员工安排。另外表中周末业务量小从而所需人员少，最大化利用人力资源，提高员工的标准劳务能力。</p>
      </el-tab-pane>
      <el-tab-pane label="日均业务量处理能力">
        <div id="lineChart" style="width: 1000px;height: 600px;"></div>
        <p style="text-align: center">从折线图-改进数据可以看出6月前24天数据波动很小，6月25日至28日这几天由于业务量极度下降，故波动较为明显，但整体来说改进后的日均业务量处理能力较为平稳，其效果较原始数据相比是优化的。</p>
      </el-tab-pane>
    </el-tabs>
  </div>
</template>

<script>
import * as echarts from 'echarts'
export default {
  name: "echarts",
  methods:{
    radarChart(){
      let myChart = echarts.init(document.getElementById('radarChart'));
      let option = {
        title: {
          text: '员工班次情况'
        },
        radar: {
          shape: 'circle',
          name: {
            textStyle: {
              color: '#000',
              borderRadius: 3,
              padding: [3, 5]
            }
          },
          indicator: [
            { name: '1', max: 25},{ name: '2', max: 25},{ name: '3', max: 25},{ name: '4', max: 25},{ name: '5', max: 25},{ name: '6', max: 25},{ name: '7', max: 25},{ name: '8', max: 25},{ name: '9', max: 25},{ name: '10', max: 25},{ name: '11', max: 25},{ name: '12', max: 25},{ name: '13', max: 25},{ name: '14', max: 25},{ name: '15', max: 25},{ name: '16', max: 25},{ name: '17', max: 25},{ name: '18', max: 25},{ name: '19', max: 25},{ name: '20', max: 25},{ name: '21', max: 25},{ name: '22', max: 25},{ name: '23', max: 25},{ name: '24', max: 25},{ name: '25', max: 25},{ name: '26', max: 25},{ name: '27', max: 25},{ name: '28', max: 25},{ name: '29', max: 25},{ name: '30', max: 25},{ name: '31', max: 25},{ name: '32', max: 25},{ name: '33', max: 25},{ name: '34', max: 25},{ name: '35', max: 25},{ name: '36', max: 25},{ name: '37', max: 25},{ name: '38', max: 25},{ name: '39', max: 25},{ name: '40', max: 25},{ name: '41', max: 25},{ name: '42', max: 25},{ name: '43', max: 25},{ name: '44', max: 25},{ name: '45', max: 25},{ name: '46', max: 25},{ name: '47', max: 25},{ name: '48', max: 25},{ name: '49', max: 25},{ name: '50', max: 25},{ name: '51', max: 25},{ name: '52', max: 25},{ name: '53', max: 25},{ name: '54', max: 25},{ name: '55', max: 25},{ name: '56', max: 25},{ name: '57', max: 25},{ name: '58', max: 25},{ name: '59', max: 25},{ name: '60', max: 25},{ name: '61', max: 25},{ name: '62', max: 25},{ name: '63', max: 25},{ name: '64', max: 25},{ name: '65', max: 25},{ name: '66', max: 25},{ name: '67', max: 25},{ name: '68', max: 25},{ name: '69', max: 25},{ name: '70', max: 25},{ name: '71', max: 25},{ name: '72', max: 25},{ name: '73', max: 25},{ name: '74', max: 25},{ name: '75', max: 25},{ name: '76', max: 25},{ name: '77', max: 25},{ name: '78', max: 25},{ name: '79', max: 25},{ name: '80', max: 25},{ name: '81', max: 25},{ name: '82', max: 25},{ name: '83', max: 25},{ name: '84', max: 25},{ name: '85', max: 25},{ name: '86', max: 25},{ name: '87', max: 25},{ name: '88', max: 25},{ name: '89', max: 25},{ name: '90', max: 25},{ name: '91', max: 25},{ name: '92', max: 25},{ name: '93', max: 25},{ name: '94', max: 25},{ name: '95', max: 25},{ name: '96', max: 25},{ name: '97', max: 25},{ name: '98', max: 25},{ name: '99', max: 25},{ name: '100', max: 25},{ name: '101', max: 25},{ name: '102', max: 25},{ name: '103', max: 25},{ name: '104', max: 25},{ name: '105', max: 25},{ name: '106', max: 25},{ name: '107', max: 25},{ name: '108', max: 25},{ name: '109', max: 25},{ name: '110', max: 25},{ name: '111', max: 25},{ name: '112', max: 25},{ name: '113', max: 25},{ name: '114', max: 25},{ name: '115', max: 25},{ name: '116', max: 25},{ name: '117', max: 25},{ name: '118', max: 25},{ name: '119', max: 25},{ name: '120', max: 25},{ name: '121', max: 25},{ name: '122', max: 25},{ name: '123', max: 25},{ name: '124', max: 25},{ name: '125', max: 25},{ name: '126', max: 25},{ name: '127', max: 25},{ name: '128', max: 25},{ name: '129', max: 25},{ name: '130', max: 25},{ name: '131', max: 25},{ name: '132', max: 25},{ name: '133', max: 25},{ name: '134', max: 25},{ name: '135', max: 25},{ name: '136', max: 25},{ name: '137', max: 25},{ name: '138', max: 25},{ name: '139', max: 25},{ name: '140', max: 25},{ name: '141', max: 25},{ name: '142', max: 25},{ name: '143', max: 25},{ name: '144', max: 25},{ name: '145', max: 25},{ name: '146', max: 25},{ name: '147', max: 25},{ name: '148', max: 25},{ name: '149', max: 25},{ name: '150', max: 25},{ name: '151', max: 25},{ name: '152', max: 25},{ name: '153', max: 25},{ name: '154', max: 25},{ name: '155', max: 25},{ name: '156', max: 25},{ name: '157', max: 25},{ name: '158', max: 25},{ name: '159', max: 25},{ name: '160', max: 25},{ name: '161', max: 25},{ name: '162', max: 25},{ name: '163', max: 25},{ name: '164', max: 25},{ name: '165', max: 25},{ name: '166', max: 25},{ name: '167', max: 25},{ name: '168', max: 25},{ name: '169', max: 25},{ name: '170', max: 25},{ name: '171', max: 25},{ name: '172', max: 25},{ name: '173', max: 25},{ name: '174', max: 25},{ name: '175', max: 25},{ name: '176', max: 25},{ name: '177', max: 25},{ name: '178', max: 25},{ name: '179', max: 25},{ name: '180', max: 25},{ name: '181', max: 25},{ name: '182', max: 25},{ name: '183', max: 25},{ name: '184', max: 25},{ name: '185', max: 25},{ name: '186', max: 25},{ name: '187', max: 25},{ name: '188', max: 25},{ name: '189', max: 25},{ name: '190', max: 25},{ name: '191', max: 25},{ name: '192', max: 25},{ name: '193', max: 25},{ name: '194', max: 25},{ name: '195', max: 25},{ name: '196', max: 25},{ name: '197', max: 25},{ name: '198', max: 25},{ name: '199', max: 25},{ name: '200', max: 25}
          ]
        },
        series: [{
          name: '员工班次情况',
          type: 'radar',
          data: [
            {
              value: [19, 19, 20, 19, 17, 18, 20, 20, 19, 20, 17, 18, 20, 18, 22, 20, 19, 18, 21, 22, 19, 19, 19, 20, 19, 21, 21, 19, 19, 20, 20, 20, 19, 20, 19, 21, 18, 18, 20, 19, 21, 20, 21, 21, 22, 16, 21, 22, 18, 21, 19, 21, 17, 18, 20, 19, 19, 21, 19, 19, 20, 20, 19, 20, 18, 20, 21, 20, 19, 19, 20, 18, 18, 18, 20, 18, 17, 20, 19, 19, 21, 19, 22, 19, 19, 19, 18, 19, 18, 20, 17, 19, 20, 19, 17, 20, 21, 18, 19, 16, 17, 21, 20, 19, 21, 19, 22, 20, 20, 17, 22, 18, 19, 20, 18, 19, 20, 22, 18, 19, 20, 21, 20, 19, 19, 19, 21, 18, 20, 21, 18, 18, 19, 18, 20, 19, 21, 20, 20, 18, 18, 19, 19, 19, 18, 18, 22, 20, 21, 18, 20, 20, 18, 18, 21, 19, 19, 20, 18, 20, 20, 17, 18, 17, 18, 19, 19, 19, 19, 19, 19, 20, 18, 20, 21, 21, 21, 22, 18, 19, 21, 18, 19, 18, 18, 19, 19, 18, 17, 19, 17, 16, 21, 20, 19, 20, 19, 20, 20, 21],
              name: '班次'
            }
          ]
        }]
      };

      myChart.setOption(option);
    },
    lineChart(){
      let myChart = echarts.init(document.getElementById('lineChart'));
      let option = {
        title: {
          text: '2020年6月日均业务处理能力表'
        },
        tooltip: {
          trigger: 'axis'
        },
        legend: {
          data: ['改进前', '改进后']
        },
        grid: {
          left: '3%',
          right: '4%',
          bottom: '3%',
          containLabel: true
        },
        toolbox: {
          feature: {
            saveAsImage: {}
          }
        },
        xAxis: {
          type: 'category',
          boundaryGap: false,
          data: [1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28]
        },
        yAxis: {
          type: 'value'
        },
        series: [
          {
            name: '改进前',
            type: 'line',
            data: [61.23478676,65.57638776,56.72117763,42.63427879,63.32653741,35.25394167,50.41235165,54.14173881,53.35162162,63.08928387,53.91289506,57.2364557,46.74872358,53.14134444,38.5943209,40.08783333,63.98813475,48.1204058,52.81879699,51.7160885,46.51948315,71.38629771,50.75791667,63.25765926,15.57344944,38.79045455,28.76517568,30.42655372]
          },
          {
            name: '改进后',
            type: 'line',
            data: [50.78006707,51.27515426,50.41882456,50.24754286,51.71667222,49.77027059,48.80344681,50.38189583,49.97493671,52.01510106,51.37581765,51.67634286,51.80263964,50.88001064,45.36525439,49.57426718,50.68723034,47.43297143,48.11575342,48.29684298,44.51864516,49.47939153,49.72204082,50.83204762,19.52164789,32.82269231,24.75143023,29.452904]
          }
        ]
      };
      myChart.setOption(option);
    },
    barChart(){
      let myChart = echarts.init(document.getElementById('barChart'));
      let app = {}
      let posList = [
        'left', 'right', 'top', 'bottom',
        'inside',
        'insideTop', 'insideLeft', 'insideRight', 'insideBottom',
        'insideTopLeft', 'insideTopRight', 'insideBottomLeft', 'insideBottomRight'
      ];

      app.configParameters = {
        rotate: {
          min: -90,
          max: 90
        },
        align: {
          options: {
            left: 'left',
            center: 'center',
            right: 'right'
          }
        },
        verticalAlign: {
          options: {
            top: 'top',
            middle: 'middle',
            bottom: 'bottom'
          }
        },
        position: {
          options: posList.reduce(function (map, pos) {
            map[pos] = pos;
            return map;
          }, {})
        },
        distance: {
          min: 0,
          max: 100
        }
      };

      app.config = {
        rotate: 90,
        align: 'left',
        verticalAlign: 'middle',
        position: 'insideBottom',
        distance: 15,
        onChange: function () {
          var labelOption = {
            normal: {
              rotate: app.config.rotate,
              align: app.config.align,
              verticalAlign: app.config.verticalAlign,
              position: app.config.position,
              distance: app.config.distance
            }
          };
          myChart.setOption({
            series: [{
              label: labelOption
            }, {
              label: labelOption
            }, {
              label: labelOption
            }, {
              label: labelOption
            }]
          });
        }
      };


      let labelOption = {
        show: true,
        position: app.config.position,
        distance: app.config.distance,
        align: app.config.align,
        verticalAlign: app.config.verticalAlign,
        rotate: app.config.rotate,
        formatter: '{c}  {name|{a}}',
        fontSize: 16,
        rich: {
          name: {
          }
        }
      };

      let option = {
        tooltip: {
          trigger: 'axis',
          axisPointer: {
            type: 'shadow'
          }
        },
        legend: {
          data: ['业务量', '出勤人数', '白班人数', '夜班人数']
        },
        toolbox: {
          show: true,
          orient: 'vertical',
          left: 'right',
          top: 'center',
          feature: {
            mark: {show: true},
            dataView: {show: true, readOnly: false},
            magicType: {show: true, type: ['line', 'bar', 'stack', 'tiled']},
            restore: {show: true},
            saveAsImage: {show: true}
          }
        },
        xAxis: [
          {
            type: 'category',
            axisTick: {show: false},
            data: ["2020/6/1","2020/6/2","2020/6/3","2020/6/4","2020/6/5","2020/6/6","2020/6/7","2020/6/8","2020/6/9","2020/6/10","2020/6/11","2020/6/12","2020/6/13","2020/6/14","2020/6/15","2020/6/16","2020/6/17","2020/6/18","2020/6/19","2020/6/20","2020/6/21","2020/6/22","2020/6/23","2020/6/24","2020/6/25","2020/6/26","2020/6/27","2020/6/28"]
          }
        ],
        yAxis: [
          {
            type: 'value'
          }
        ],
        series: [
          {
            name: '业务量',
            type: 'bar',
            barGap: 0,
            emphasis: {
              focus: 'series'
            },
            data: [8327.931,9639.729,8621.619,7034.656,9309.001,4230.473,4587.524,7254.993,7896.04,9778.839,8733.889,9043.36,5750.093,4782.721,5171.639,6494.229,9022.327,6640.616,7024.9,5843.918,4140.234,9351.605,7309.14,8539.784,1386.037,2986.865,2128.623,3681.613]
          },
          {
            name: '出勤人数',
            type: 'bar',
            emphasis: {
              focus: 'series'
            },
            data: [164,188,171,140,180,85,94,144,158,188,170,175,111,94,114,131,178,140,146,121,93,189,147,168,71,91,86,125]
          },
          {
            name: '白班人数',
            type: 'bar',
            emphasis: {
              focus: 'series'
            },
            data: [82,93,86,70,90,42,48,72,79,94,84,87,55,47,72,79,94,84,87,55,47,96,72,84,36,48,43,63]
          },
          {
            name: '夜班人数',
            type: 'bar',
            emphasis: {
              focus: 'series'
            },
            data: [82,95,85,70,90,43,46,72,79,94,86,88,56,47,72,79,94,86,88,56,47,93,75,84,35,43,43,62]
          }
        ]
      }
      myChart.setOption(option)
    }
  },
  mounted() {
    this.radarChart();
    this.lineChart();
    this.barChart()
  }
}
</script>

<style lang="scss">
.mod-demo-echarts {
  > .el-alert {
    margin-bottom: 10px;
  }
  > .el-row {
    margin-top: -10px;
    margin-bottom: -10px;
    .el-col {
      padding-top: 10px;
      padding-bottom: 10px;
    }
  }
  .chart-box {
    min-height: 400px;
  }
}
</style>
