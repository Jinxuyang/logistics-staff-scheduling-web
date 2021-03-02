<template>
  <div class="Echarts">
    <el-tabs tab-position="top" >
      <el-tab-pane label="第一周">
        <div id="lineChartWeek" style="width: 900px;height: 540px;margin-left: 150px"></div>
        <el-card style="margin-left: 150px;margin-right: 150px">
          <div slot="header" class="clearfix">
            <span>
              <svg t="1614651366943" class="icon" viewBox="0 0 1080 1024" version="1.1" xmlns="http://www.w3.org/2000/svg" p-id="7216" width="17" height="17"><path d="M227.4304 947.5712a44.2368 44.2368 0 0 1-44.176-45.02506667V672.5632a44.96533333 44.96533333 0 1 1 89.08053334 0v229.98293333a44.90453333 44.90453333 0 0 1-44.90453334 45.02506667z m221.54773334 0a44.2368 44.2368 0 0 1-44.1152-45.02506667V538.336a44.90453333 44.90453333 0 0 1 89.08053333 0v363.4816a44.90453333 44.90453333 0 0 1-44.90453333 45.7536z m221.6096 0a44.2368 44.2368 0 0 1-44.11626667-45.02506667v-159.95733333a44.90453333 44.90453333 0 0 1 89.08053333 0v159.95733333a44.90453333 44.90453333 0 0 1-44.90453333 45.02506667z m221.60853333 0a44.2368 44.2368 0 0 1-44.176-45.02506667v-294.912a44.96533333 44.96533333 0 1 1 89.14133333 0v298.61333334a44.90453333 44.90453333 0 0 1-44.90453333 41.264zM169.23733334 501.44106667a44.176 44.176 0 0 1-36.0448-17.6576 45.02613333 45.02613333 0 0 1 11.0432-62.6848l320.21653333-246.9728a45.57226667 45.57226667 0 0 1 55.22026667 0l147.27466666 120.14933333 237.81013334-198.368a44.53973333 44.53973333 0 0 1 57.4048 67.84213333L697.8336 386.45013333a44.1152 44.1152 0 0 1-56.67733333 0l-147.2128-120.93866666-294.54826667 226.3424a45.57226667 45.57226667 0 0 1-30.15786666 9.5872z" p-id="7217"></path><path d="M933.4592 325.2224a44.90453333 44.90453333 0 0 1-44.90453333-44.2368v-123.85066667H763.37066667a44.96533333 44.96533333 0 0 1 0-89.20213333h170.09066667a44.90453333 44.90453333 0 0 1 44.90346666 44.176v168.8768a44.90453333 44.90453333 0 0 1-44.90453333 44.2976z" p-id="7218"></path></svg>
              分析
            </span>
          </div>
          <div >
            <p style="text-align: center;font-size: 15px">从折线图-改进数据可以看出6月份第一周周内各组出勤率均在60%以上,并且各组周内平均出勤率为84%，周末由于业务量下滑，出勤率也对应有所降低，保证人员的最大化利用，减少人力成本</p>
          </div>
        </el-card>
      </el-tab-pane>
      <el-tab-pane label="第二周">
        <div style="width: 1000px;height: 600px;"></div>
        <p style  ="text-align: center">无数据</p>
      </el-tab-pane>
      <el-tab-pane label="第三周">
        <div style="width: 1000px;height: 600px;"></div>
        <p style="text-align: center">无数据</p>
      </el-tab-pane>
      <el-tab-pane label="第四周">
        <div style="width: 1000px;height: 600px;"></div>
        <p style="text-align: center">无数据</p>
      </el-tab-pane>
    </el-tabs>
  </div>
</template>

<script>
import * as echarts from 'echarts'
export default {
  name: "echarts",
  methods:{
    lineChart(){
      let myChart = echarts.init(document.getElementById('lineChartWeek'));
      let option = {
        title: {
          text: '第一周计划出勤率'
        },
        tooltip: {
          trigger: 'axis'
        },
        legend: {
          data: ["收货组","补货组","拣货组","分货组","复核组","包装组","订单组","物流组"]
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
          data: ['周一', '周二', '周三', '周四', '周五', '周六', '周日']
        },
        yAxis: {
          type: 'value',
          data: ['0', '0.2', '0.4', '0.6', '0.8', '1.0']

        },
        series: [
          {
            name: '收货组',
            type: 'line',
            data: [0.8,0.96,0.84,0.68,0.92,0.4,0.52]
          },
          {
            name: '补货组',
            type: 'line',
            data: [0.75,0.9,0.85,0.85,0.95,0.5,0.4]
          },
          {
            name: '拣货组',
            type: 'line',
            data: [0.83,0.96,0.86,0.76,0.9,0.33,0.53]
          },
          {
            name: '分货组',
            type: 'line',
            data: [0.8,0.92,0.8,0.68,0.92,0.32,0.48]
          },
          {
            name: '复核组',
            type: 'line',
            data: [0.84,0.96,0.92,0.76,0.92,0.24,0.52]
          },
          {
            name: '包装组',
            type: 'line',
            data: [0.68,0.92,0.92,0.64,0.92,0.6,0.44]
          },
          {
            name: '订单组',
            type: 'line',
            data: [0.88,0.88,0.88,0.64,0.92,0.44,0.48]
          },
          {
            name: '物流组',
            type: 'line',
            data: [0.96,1,0.76,0.6,0.76,0.6,0.36]
          }
        ]
      };
      myChart.setOption(option);
    }

  },
  mounted() {
    this.lineChart();
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
