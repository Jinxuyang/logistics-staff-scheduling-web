<template>
  <div class="mod-config">


    <el-form :inline="true" :model="dataForm" @keyup.enter.native="getDataList()">
      <el-form-item>
        <el-input v-model="dataForm.key" placeholder="员工编号" clearable></el-input>
      </el-form-item>
      <el-form-item>
        <el-select v-model="dataForm.category" placeholder="组别">
<!--          <el-option label="全部" value="全部"></el-option>-->
          <el-option label="收货组" value="收货组"></el-option>
          <el-option label="补货组" value="补货组"></el-option>
          <el-option label="拣货组" value="拣货组"></el-option>
          <el-option label="分拣组" value="分拣组"></el-option>
          <el-option label="复核组" value="复核组"></el-option>
          <el-option label="包装组" value="包装组"></el-option>
          <el-option label="订单组" value="订单组"></el-option>
          <el-option label="物流组" value="物流组"></el-option>
        </el-select>
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
        <el-button v-if="isAuth('generator:scheduling:save')" type="primary" @click="addOrUpdateHandle()">新增</el-button>
        <el-button v-if="isAuth('generator:scheduling:delete')" type="danger" @click="deleteHandle()" :disabled="dataListSelections.length <= 0">批量删除</el-button>
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
      <el-table-column
        fixed="right"
        header-align="center"
        align="center"
        width="150"
        label="操作">
        <template slot-scope="scope">
          <el-button type="text" size="small" @click="setGlobalRowUsername(scope.row.username)">备注</el-button>
          <el-button type="text" size="small" @click="deleteHandle(scope.row.id)">删除</el-button>
        </template>
      </el-table-column>
    </el-table>
    <!-- 弹窗, 新增 / 修改 -->
    <add-or-update v-if="addOrUpdateVisible" ref="addOrUpdate" @refreshDataList="getDataList"></add-or-update>
    <div>
      <el-dialog :visible.sync="dialogFormVisible">
        <el-form>
          <el-form-item label="备注">
            <el-input v-model="dataForm.remark" autocomplete="off"></el-input>
          </el-form-item>
        </el-form>
        <div slot="footer" class="dialog-footer">
          <el-button @click="dialogFormVisible = false">取 消</el-button>
          <el-button type="primary" @click="addRemark()">确 定</el-button>
        </div>
      </el-dialog>
    </div>
  </div>
</template>

<script>
import AddOrUpdate from './scheduling-add-or-update'
export default {
  data () {
    return {
      dataForm: {
        key: '',
        category: '拣货组',
        date: 1,
        remark: ''
      },
      dataList: [],
      dataListLoading: false,
      dataListSelections: [],
      addOrUpdateVisible: false,
      dialogFormVisible: false,
      rowUsername: ''
    }
  },
  components: {
    AddOrUpdate
  },
  activated () {
    this.getDataList()
  },
  methods: {
    // 获取数据列表
    getDataList () {
      this.dataListLoading = true
      this.$http({
        url: this.$http.adornUrl('/generator/scheduling/week-list'),
        method: 'get',
        params: this.$http.adornParams({
          'key': this.dataForm.key,
          'category': this.dataForm.category,
          'week': this.dataForm.date
        })
      }).then(({data}) => {
        if (data && data.code === 0) {
          this.dataList = data.data
          console.log(data)
          //this.totalPage = data.page.totalCount
        } else {
          this.dataList = []
          this.totalPage = 0
        }
        this.dataListLoading = false
      })
    },
    // 新增 / 修改
    addOrUpdateHandle (id) {
      this.addOrUpdateVisible = true
      this.$nextTick(() => {
        this.$refs.addOrUpdate.init(id)
      })
    },
    addRemark(){
      this.$http({
        url: this.$http.adornUrl('/generator/weekscheduleremark/update'),
        method: 'post',
        params: this.$http.adornParams({
          'username': this.rowUsername,
          'week': this.dataForm.date,
          'remark': this.dataForm.remark
        })
      }).then(({data}) => {
        if (data && data.code === 0) {
          this.dataList = data.data
          console.log(data)
        } else {
          this.dataList = []
          this.totalPage = 0
        }
        this.dialogFormVisible = false
        this.getDataList()
      })
    },
    setGlobalRowUsername(username){
      this.dialogFormVisible = true
      this.rowUsername = username
    },
    // 删除
    deleteHandle (id) {
      var ids = id ? [id] : this.dataListSelections.map(item => {
        return item.id
      })
      this.$confirm(`确定对[id=${ids.join(',')}]进行[${id ? '删除' : '批量删除'}]操作?`, '提示', {
        confirmButtonText: '确定',
        cancelButtonText: '取消',
        type: 'warning'
      }).then(() => {
        this.$http({
          url: this.$http.adornUrl('/generator/scheduling/delete'),
          method: 'post',
          data: this.$http.adornData(ids, false)
        }).then(({data}) => {
          if (data && data.code === 0) {
            this.$message({
              message: '操作成功',
              type: 'success',
              duration: 1500,
              onClose: () => {
                this.getDataList()
              }
            })
          } else {
            this.$message.error(data.msg)
          }
        })
      })
    }
  }
}
</script>
