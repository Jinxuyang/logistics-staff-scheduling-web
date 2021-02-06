<template>
  <div >
    <el-calendar >
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
  </div>
</template>

<script>
export default {
  name: "personal-info",
  data () {
    return {
      user_id: '',
      schedule:''
    }
  },
  methods: {
    async getSchedule(){
      await this.$http({
        url: this.$http.adornUrl('/sys/user/info'),
        method: 'get',
      }).then(({data}) => {
        let reg = new RegExp("staff([0-9]*)")
        this.user_id = reg.exec(data.user.username)[1]
      })
      this.$http({
        url: this.$http.adornUrl("/generator/scheduling/listByUserID/"+this.user_id),
        method: 'get',
      }).then(({data}) => {
        this.schedule = data.data
        console.log(this.schedule)
      })
    },
  },
  created () {
    this.getSchedule()
  },
  computed: {
    formatSchedule() {
      return data => {
        return this.schedule.filter(ele => {
          if (ele.date == data.day.split('-')[2]){
            return true
          } else {
            return false
          }
        })
      }
    }
  }
}
</script>

<style scoped>

</style>
