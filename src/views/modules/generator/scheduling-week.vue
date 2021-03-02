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
<!--    <el-row style="margin-bottom: 20px;text-align: center">
      <el-button type="success" size="big" circle>
        <svg t="1614650981025" class="icon" viewBox="0 0 1024 1024" version="1.1" xmlns="http://www.w3.org/2000/svg" p-id="2158" width="15" height="15"><path d="M512 743.21c-127.49 0-231.21-103.71-231.21-231.21S384.51 280.79 512 280.79 743.21 384.51 743.21 512 639.49 743.21 512 743.21z m0-400.76c-93.49 0-169.55 76.06-169.55 169.55S418.51 681.55 512 681.55 681.55 605.49 681.55 512 605.49 342.45 512 342.45zM512 242.26c-17.02 0-30.83-13.8-30.83-30.83V95.83C481.17 78.8 494.98 65 512 65s30.83 13.8 30.83 30.83v115.6c0 17.03-13.81 30.83-30.83 30.83zM299.46 330.29c-7.89 0-15.78-3.01-21.8-9.03l-81.74-81.74c-12.04-12.04-12.04-31.55 0-43.59s31.55-12.04 43.59 0l81.74 81.74c12.04 12.04 12.04 31.55 0 43.59-6.02 6.02-13.9 9.03-21.79 9.03zM211.43 542.83H95.83C78.8 542.83 65 529.02 65 512s13.8-30.83 30.83-30.83h115.6c17.02 0 30.83 13.8 30.83 30.83s-13.8 30.83-30.83 30.83zM217.72 837.1c-7.89 0-15.78-3.01-21.8-9.03-12.04-12.04-12.04-31.55 0-43.59l81.74-81.74c12.04-12.04 31.55-12.04 43.59 0 12.04 12.04 12.04 31.55 0 43.59l-81.74 81.74c-6.01 6.02-13.9 9.03-21.79 9.03zM512 959c-17.02 0-30.83-13.8-30.83-30.83v-115.6c0-17.02 13.8-30.83 30.83-30.83s30.83 13.8 30.83 30.83v115.6c0 17.03-13.81 30.83-30.83 30.83zM806.28 837.1c-7.89 0-15.78-3.01-21.8-9.03l-81.74-81.74c-12.04-12.04-12.04-31.55 0-43.59 12.04-12.04 31.55-12.04 43.59 0l81.74 81.74c12.04 12.04 12.04 31.55 0 43.59a30.728 30.728 0 0 1-21.79 9.03zM928.17 542.83h-115.6c-17.02 0-30.83-13.8-30.83-30.83s13.8-30.83 30.83-30.83h115.6c17.02 0 30.83 13.8 30.83 30.83s-13.8 30.83-30.83 30.83zM724.54 330.29c-7.89 0-15.78-3.01-21.8-9.03-12.04-12.04-12.04-31.55 0-43.59l81.74-81.74c12.04-12.04 31.55-12.04 43.59 0 12.04 12.04 12.04 31.55 0 43.59l-81.74 81.74c-6.01 6.02-13.9 9.03-21.79 9.03z" p-id="2159"></path></svg>
      </el-button>
      <el-button type="warning" size="big" circle>
        <svg t="1614651060541" class="icon" viewBox="0 0 1024 1024" version="1.1" xmlns="http://www.w3.org/2000/svg" p-id="3497" width="15" height="15"><path d="M467.648 927.008A412 412 0 0 1 133.808 755.632a31.408 31.408 0 0 1 27.76-49.6l5.136 0.368c5.6 0.368 11.2 0.784 16.864 0.784 191.168 0.272 346.48-154.24 347.2-345.392a341.744 341.744 0 0 0-64.752-200.352 31.376 31.376 0 0 1 27.664-49.6c221.216 12.256 392.192 198.864 385.12 420.304-7.072 221.44-189.6 396.736-411.152 394.864z m-240.24-159.296a345.968 345.968 0 1 0 325.536-583.328 402.56 402.56 0 0 1 40.976 177.424c-0.72 208.992-158.672 383.92-366.512 405.904z" fill="#000000" p-id="3498"></path></svg>
      </el-button>
      <el-button type="info" size="big" circle>
        <svg t="1614651129624" class="icon" viewBox="0 0 1024 1024" version="1.1" xmlns="http://www.w3.org/2000/svg" p-id="5222" width="15" height="15s"><path d="M327.68 112.64a30.72 30.72 0 0 1 30.69952 29.568L358.4 143.36v122.88a30.72 30.72 0 0 1-61.41952 1.152L296.96 266.24V143.36a30.72 30.72 0 0 1 30.72-30.72zM450.56 112.64a30.72 30.72 0 0 1 30.69952 29.568L481.28 143.36v122.88a30.72 30.72 0 0 1-61.41952 1.152L419.84 266.24V143.36a30.72 30.72 0 0 1 30.72-30.72zM573.44 112.64a30.72 30.72 0 0 1 30.69952 29.568L604.16 143.36v122.88a30.72 30.72 0 0 1-61.41952 1.152L542.72 266.24V143.36a30.72 30.72 0 0 1 30.72-30.72zM788.48 849.92a30.72 30.72 0 0 1 1.152 61.41952L788.48 911.36H112.64a30.72 30.72 0 0 1-1.152-61.41952L112.64 849.92h675.84z" fill="#000000" p-id="5223"></path><path d="M788.48 358.4a30.72 30.72 0 0 1 30.69952 29.568L819.2 389.12v184.31488c0.0256 144.10752-83.9168 275.0208-214.8864 335.13984a30.72 30.72 0 1 1-25.63072-55.83872 307.25632 307.25632 0 0 0 179.05664-275.69664L757.76 573.44l-0.00512-153.6h-614.4L143.36 573.44512a307.25632 307.25632 0 0 0 175.81056 277.77024l3.26656 1.52064a30.72 30.72 0 1 1-25.63584 55.83872c-129.65888-59.52-213.2224-188.42112-214.85568-330.81344L81.92 573.44V389.12a30.72 30.72 0 0 1 29.568-30.69952L112.64 358.4h675.84z" fill="#000000" p-id="5224"></path><path d="M788.48 358.4c83.98336 0 152.22272 67.39968 153.57952 151.06048L942.08 512v30.72c0 83.98336-67.39968 152.22272-151.06048 153.57952L788.48 696.32h-12.97408a30.72 30.72 0 0 1-1.152-61.41952l1.152-0.02048H788.48c50.3296 0 91.2384-40.3456 92.14464-90.4704L880.64 542.72v-30.72c0-50.89792-41.26208-92.16-92.16-92.16a30.72 30.72 0 1 1 0-61.44z" fill="#000000" p-id="5225"></path></svg>
      </el-button>
    </el-row>-->
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
