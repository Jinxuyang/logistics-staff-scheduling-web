<template>
  <div class="Echarts">
    <el-tabs tab-position="left" >
      <el-tab-pane label="第一周">
        <div id="lineChartWeek" style="width: 1000px;height: 600px;"></div>
        <p style="text-align: center">从折线图-改进数据可以看出6月份第一周周内各组出勤率均在60%以上,并且各组周内平均出勤率为84%，周末由于业务量下滑，出勤率也对应有所降低，保证人员的最大化利用，减少人力成本</p>
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
          text: '2020年6月第一周计划出勤率'
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
