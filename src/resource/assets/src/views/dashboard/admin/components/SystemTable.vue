<template>
  <el-table 
    :data="list" 
    :header-cell-style="{background:'#eef1f6',color:'#606266'}"
    class="system-table">
    <el-table-column label="系统信息" width="200">
      <template slot-scope="scope">
        {{ scope.row.name }}
      </template>
    </el-table-column>
    <el-table-column label="" min-width="100" align="left">
      <template slot-scope="scope">
        {{ scope.row.content }}
      </template>
    </el-table-column>
  </el-table>
</template>

<script>
import { getInfo } from '@/api/system'

export default {
  filters: {
    contentFilter(str) {
      return str.substring(0, 30)
    }
  },
  data() {
    return {
      list: null
    }
  },
  created() {
    this.fetchData()
  },
  methods: {
    fetchData() {
      getInfo().then(response => {
        const data = response.data

        const list = [
            {
              name: '当前版本',
              content: data.admin.name + ' v' + data.admin.version,
            },
            {
              name: '服务器域名/IP',
              content: data.system.domain + ' / ' + data.system.ip,
            },
            {
              name: '服务器信息',
              content: data.system.php_uname,
            },
            {
              name: '服务器环境',
              content: data.system.web_server,
            },
            {
              name: 'PHP 版本',
              content: data.system.php_version,
            },
            {
              name: 'MySQL 版本',
              content: data.system.mysql_version,
            },
            {
              name: '最大上传限制',
              content: data.system.file_upload,
            },
            {
              name: '服务器时间',
              content: data.system.time,
            }  
          ]
                  
        this.list = list
      })
    }
  }
}
</script>

<style lang="scss" scoped>
.system-table {
  width: 100%;
  -webkit-box-shadow: 4px 4px 40px rgba(0, 0, 0, 0.05);
  box-shadow: 4px 4px 40px rgba(0, 0, 0, 0.05);
  border-color: rgba(0, 0, 0, 0.05);
}
</style>
