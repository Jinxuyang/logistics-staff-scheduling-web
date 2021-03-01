<template>
  <div class="mod-config">


    <el-form :inline="true" :model="dataForm" @keyup.enter.native="getDataList()">
      <el-form-item>
        <el-input v-model="dataForm.key" placeholder="员工编号" clearable></el-input>
      </el-form-item>
      <el-form-item>
        <el-select v-model="dataForm.date" placeholder="周数">
          <el-option label="第一周" value="1"></el-option>
          <el-option label="第二周" value="2"></el-option>
          <el-option label="第三周" value="3"></el-option>
          <el-option label="第四周" value="4"></el-option>
        </el-select>
      </el-form-item>
      <el-form-item>
        <el-button @click="getDataList()">查询</el-button>
      </el-form-item>
    </el-form>
    <el-table
      :data="dataList"
      border
      v-loading="dataListLoading"

      style="width: 100%;">
      <!--      <el-table-column
              type="selection"
              header-align="center"
              align="center"
              width="50">
            </el-table-column>-->
      <el-table-column
        prop="username"
        header-align="center"
        align="center"
        label="员工ID">
      </el-table-column>
      <el-table-column
        prop="category"
        header-align="center"
        align="center"
        label="组别">
      </el-table-column>
      <el-table-column
        prop="date[0]"
        header-align="center"
        align="center"
        label="星期一"
        width="70px">
        <template slot-scope="scope">
          <div slot="reference" class="name-wrapper" >
            <el-tag size="success" v-if="scope.row.date[0] === '白班'" >{{ scope.row.date[0] }}</el-tag>
            <el-tag size="warning" v-else-if="scope.row.date[0] === '夜班'" >{{ scope.row.date[0] }}</el-tag>
            <el-tag size="info" v-else="scope.row.status === '休息'" >{{ scope.row.date[0] }}</el-tag>
          </div>
        </template>
      </el-table-column>
      <el-table-column
        prop="date[1]"
        header-align="center"
        align="center"
        label="星期二"
        width="70px">
        <template slot-scope="scope">
          <div slot="reference" class="name-wrapper" >
            <el-tag size="success" v-if="scope.row.date[1] === '白班'" >{{ scope.row.date[1] }}</el-tag>
            <el-tag size="warning" v-else-if="scope.row.date[1] === '夜班'" >{{ scope.row.date[1] }}</el-tag>
            <el-tag size="info" v-else="scope.row.status === '休息'" >{{ scope.row.date[1] }}</el-tag>
          </div>
        </template>
      </el-table-column>
      <el-table-column
        prop="date[2]"
        header-align="center"
        align="center"
        label="星期三"
        width="70px">
        <template slot-scope="scope">
          <div slot="reference" class="name-wrapper" >
            <el-tag size="success" v-if="scope.row.date[2] === '白班'" >{{ scope.row.date[2] }}</el-tag>
            <el-tag size="warning" v-else-if="scope.row.date[2] === '夜班'" >{{ scope.row.date[2] }}</el-tag>
            <el-tag size="info" v-else="scope.row.status === '休息'" >{{ scope.row.date[2] }}</el-tag>
          </div>
        </template>
      </el-table-column>
      <el-table-column
        prop="date[3]"
        header-align="center"
        align="center"
        label="星期四"
        width="70px">
        <template slot-scope="scope">
          <div slot="reference" class="name-wrapper" >
            <el-tag size="success" v-if="scope.row.date[3] === '白班'" >{{ scope.row.date[3] }}</el-tag>
            <el-tag size="warning" v-else-if="scope.row.date[3] === '夜班'" >{{ scope.row.date[3] }}</el-tag>
            <el-tag size="info" v-else="scope.row.status === '休息'" >{{ scope.row.date[3] }}</el-tag>
          </div>
        </template>
      </el-table-column>
      <el-table-column
        prop="date[4]"
        header-align="center"
        align="center"
        label="星期五"
        width="70px">
        <template slot-scope="scope">
          <div slot="reference" class="name-wrapper" >
            <el-tag size="success" v-if="scope.row.date[4] === '白班'" >{{ scope.row.date[4] }}</el-tag>
            <el-tag size="warning" v-else-if="scope.row.date[4] === '夜班'" >{{ scope.row.date[4] }}</el-tag>
            <el-tag size="info" v-else="scope.row.status === '休息'" >{{ scope.row.date[4] }}</el-tag>
          </div>
        </template>
      </el-table-column>
      <el-table-column
        prop="date[5]"
        header-align="center"
        align="center"
        label="星期六"
        width="70px">
        <template slot-scope="scope">
          <div slot="reference" class="name-wrapper" >
            <el-tag size="success" v-if="scope.row.date[5] === '白班'" >{{ scope.row.date[5] }}</el-tag>
            <el-tag size="warning" v-else-if="scope.row.date[5] === '夜班'" >{{ scope.row.date[5] }}</el-tag>
            <el-tag size="info" v-else="scope.row.status === '休息'" >{{ scope.row.date[5] }}</el-tag>
          </div>
        </template>
      </el-table-column>
      <el-table-column
        prop="date[6]"
        header-align="center"
        align="center"
        label="星期天"
        width="70px">
        <template slot-scope="scope">
          <div slot="reference" class="name-wrapper" >
            <el-tag size="success" v-if="scope.row.date[6] === '白班'" >{{ scope.row.date[6] }}</el-tag>
            <el-tag size="warning" v-else-if="scope.row.date[6] === '夜班'" >{{ scope.row.date[6] }}</el-tag>
            <el-tag size="info" v-else="scope.row.status === '休息'" >{{ scope.row.date[6] }}</el-tag>
          </div>
        </template>
      </el-table-column>
      <el-table-column
        prop="day"
        header-align="center"
        align="center"
        label="累计白班">
      </el-table-column>
      <el-table-column
        prop="night"
        header-align="center"
        align="center"
        label="累计夜班">
      </el-table-column>
      <el-table-column
        prop="rest"
        header-align="center"
        align="center"
        label="累计休息">
      </el-table-column>
      <el-table-column
        prop="remark"
        header-align="center"
        align="center"
        label="备注">
      </el-table-column>
    </el-table>

  </div>
</template>

<script>
export default {
  data () {
    return {
      dataForm: {
        key: '',
        category: '拣货组',
        date: 1,
        remark: ''
      },
      personalInfo: '',
      dataList: [],
      dataListLoading: false,
      dataListSelections: [],
    }
  },
  activated () {
    this.getPersonalInfo()
    //this.getDataList()
  },
  methods: {
    async getPersonalInfo(){
      await this.$http({
        url: this.$http.adornUrl('/sys/user/info'),
        method: 'get',
      }).then(({data}) => {
        this.personalInfo = data.user
        this.getDataList();
      })
    },
    // 获取数据列表
    getDataList () {
      this.dataListLoading = true
      this.$http({
        url: this.$http.adornUrl('/generator/scheduling/week-list'),
        method: 'get',
        params: this.$http.adornParams({
          'key': this.dataForm.key,
          'category': this.personalInfo.category,
          'week': this.dataForm.date
        })
      }).then(({data}) => {
        if (data && data.code === 0) {
          this.dataList = data.data
          console.log(data)
        } else {
          this.dataList = []
          this.totalPage = 0
        }
        this.dataListLoading = false
      })
    },
  }
}
</script>
