<template>
  <div class="Echarts">
    <el-tabs tab-position="left" >
      <el-tab-pane label="员工班次情况">
        <div id="main" style="width: 1000px;height: 600px;"></div>
        <p style="text-align: center">从图中可以看出整体的28天出勤员工班次数量极值差是较小的，200名员工班次数量均在16-22范围之间</p>
      </el-tab-pane>
      <el-tab-pane label="白夜班出勤人数分析">配置管理</el-tab-pane>
      <el-tab-pane label="日均业务量处理能力">角色管理</el-tab-pane>
    </el-tabs>
  </div>
</template>

<script>
import * as echarts from 'echarts'
export default {
  name: "echarts",
  methods:{
    myEcharts(){
      var myChart = echarts.init(document.getElementById('main'));
      var option = {
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

      // 使用刚指定的配置项和数据显示图表。
      myChart.setOption(option);
    }
  },
  mounted() {
    this.myEcharts()
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
