<template>
  <div >
    <el-calendar>
      <template
        slot="dateCell"
        slot-scope="{date, data}">
        <p :class="data.isSelected ? 'is-selected' : ''">
          {{ data.day.split('-')[2]}}
        </p>
        <el-popover
          placement="right"
          width="400" height="400">
          <el-table :data="usersInfo">
            <el-table-column width="100" property="username" label="姓名"></el-table-column>
            <el-table-column width="100" property="mobile" label="电话"></el-table-column>
            <el-table-column width="100" property="email" label="邮箱"></el-table-column>
          </el-table>
          <div slot="reference" v-on:click="getSameStatusUsers(data.day.split('-')[2])">
            <p v-for="(info ,index) in formatSchedule(data)" :key="index">
              <el-tag size="success" v-if="info.status === '白班'" >{{ info.status }}</el-tag>
              <el-tag size="warning" v-else-if="info.status === '夜班'" >{{ info.status }}</el-tag>
              <el-tag size="info" v-else >{{ info.status }}</el-tag>
            </p>
          </div>
        </el-popover>
      </template>
    </el-calendar>
  </div>
</template>

<script>
export default {
  name: "personal-info",
  data () {
    return {
      user_id: '',
      schedule:'',
      usersInfo:[],
      personalInfo:''
    }
  },
  methods: {
    async getSchedule(){
      await this.$http({
        url: this.$http.adornUrl('/sys/user/info'),
        method: 'get',
      }).then(({data}) => {
        this.personalInfo = data.user
        let reg = new RegExp("staff([0-9]*)")
        this.user_id = reg.exec(this.personalInfo.username)[1]
      })
      this.$http({
        url: this.$http.adornUrl("/generator/scheduling/listByUserID/"+this.user_id),
        method: 'get',
      }).then(({data}) => {
        this.schedule = data.data
        console.log(this.schedule)
      })
    },
    getSameStatusUsers(day){
      console.log("来了")
      this.$http({
        url: this.$http.adornUrl("/generator/scheduling/listSameStatusUsers"),
        method: 'get',
        params: this.$http.adornParams({
          userId: this.personalInfo.userId,
          day: day
        })
      }).then(({data}) => {
        this.usersInfo = data.data
        console.log(this.usersInfo)
      })
    }
  },
  created () {
    this.getSchedule()
  },
  computed: {
    formatSchedule() {
      return data => {
        return this.schedule.filter(ele => {
          return ele.date == data.day.split('-')[2];
        })
      }
    }
  }
}
</script>

<style scoped>

</style>
