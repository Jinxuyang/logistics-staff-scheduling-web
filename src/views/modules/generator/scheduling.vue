<template>
  <div class="mod-config">
    <el-form :inline="true" :model="dataForm" @keyup.enter.native="getDataList()">
      <el-form-item>
        <el-input v-model="dataForm.key" placeholder="参数名" clearable></el-input>
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
        <el-button @click="getDataList()">查询</el-button>
        <el-button v-if="isAuth('generator:scheduling:save')" type="primary" @click="addOrUpdateHandle()">新增</el-button>
        <el-button v-if="isAuth('generator:scheduling:delete')" type="danger" @click="deleteHandle()" :disabled="dataListSelections.length <= 0">批量删除</el-button>
      </el-form-item>
    </el-form>
    <el-table
      :data="dataList"
      border
      v-loading="dataListLoading"
      @selection-change="selectionChangeHandle"
      style="width: 100%;">
      <el-table-column
        type="selection"
        header-align="center"
        align="center"
        width="50">
      </el-table-column>
      <el-table-column
        prop="userId"
        header-align="center"
        align="center"
        label="ID"
        width="70">
      </el-table-column>
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
        label="员工ID">
      </el-table-column>
      <el-table-column
        header-align="center"
        align="center"
        label="排班情况">
        <template slot-scope="scope">
          <el-button
            size="mini"
            @click="getSchedule(scope.row.username)">
            点击查看排班情况
          </el-button>
        </template>
      </el-table-column>
    </el-table>
    <el-pagination
      @size-change="sizeChangeHandle"
      @current-change="currentChangeHandle"
      :current-page="pageIndex"
      :page-sizes="[10, 20, 50, 100]"
      :page-size="pageSize"
      :total="totalPage"
      layout="total, sizes, prev, pager, next, jumper">
    </el-pagination>
    <!-- 弹窗, 新增 / 修改 -->
    <add-or-update v-if="addOrUpdateVisible" ref="addOrUpdate" @refreshDataList="getDataList"></add-or-update>

    <div>
      <el-dialog
        title="提示"
        :visible.sync="dialogVisible">
        <el-calendar>
          <template
            slot="dateCell"
            slot-scope="{date, data}">
            <p :class="data.isSelected ? 'is-selected' : ''">
              {{ data.day.split('-')[2]}}
            </p>
            <p v-for="(info ,index) in formatSchedule(data)" :key="index">
              <el-tag size="success" v-if="info.status === '白班'" >{{ info.status }}</el-tag>
              <el-tag size="warning" v-else-if="info.status === '夜班'" >{{ info.status }}</el-tag>
              <el-tag size="info" v-else >{{ info.status }}</el-tag>
            </p>
          </template>
        </el-calendar>
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
          category: '拣货组'
        },
        dataList: [],
        pageIndex: 1,
        pageSize: 10,
        totalPage: 0,
        dataListLoading: false,
        dataListSelections: [],
        addOrUpdateVisible: false,
        dialogVisible: false,
        schedule:''
      }
    },
    components: {
      AddOrUpdate
    },
    activated () {
      this.getDataList()
    },
    computed: {
      formatSchedule() {
        return data => {
          return this.schedule.filter(ele => {
            return ele.date == data.day.split('-')[2];
          })
        }
      }
    },
    methods: {
      // 获取数据列表
      getDataList () {
        this.dataListLoading = true
        this.$http({
          url: this.$http.adornUrl('/sys/user/list'),
          method: 'get',
          params: this.$http.adornParams({
            'page': this.pageIndex,
            'limit': this.pageSize,
            'category': this.dataForm.category,
          })
        }).then(({data}) => {
          if (data && data.code === 0) {
            this.dataList = data.page.list
            this.totalPage = data.page.totalCount
          } else {
            this.dataList = []
            this.totalPage = 0
          }
          this.dataListLoading = false
        })
      },
      // 每页数
      sizeChangeHandle (val) {
        this.pageSize = val
        this.pageIndex = 1
        this.getDataList()
      },
      // 当前页
      currentChangeHandle (val) {
        this.pageIndex = val
        this.getDataList()
      },
      // 多选
      selectionChangeHandle (val) {
        this.dataListSelections = val
      },
      // 新增 / 修改
      addOrUpdateHandle (id) {
        this.addOrUpdateVisible = true
        this.$nextTick(() => {
          this.$refs.addOrUpdate.init(id)
        })
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
      },
      async getSchedule(username){
        this.dialogVisible = true
        console.log(username)
        this.$http({
          url: this.$http.adornUrl("/generator/scheduling/listByUsername"),
          method: 'get',
          params: this.$http.adornParams({
            'username': username
          })
        }).then(({data}) => {
          this.schedule = data.data
          console.log(this.schedule)
        })
      },
    }
  }
</script>
