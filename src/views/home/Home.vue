<template>
  <el-container>
    <el-header class="home-header">
      <el-row>
        <el-col :span="4"><div class="grid-content bg-purple"><img src="" alt=""></div></el-col>
        <el-col :span="16"><div class="grid-content bg-purple"><h2>电商后台管理</h2></div></el-col>

        <el-col :span="4"><div class="grid-content bg-purple loginout"><a href="#" @click.prevent="logout">退出</a></div></el-col>
      </el-row>
    </el-header>
    <el-container>
      <el-aside width="200px" class="home-aside">Aside</el-aside>
      <el-main class="home-content"></el-main>
    </el-container>
  </el-container>
</template>

<script>
export default {
  data () {
    return {

    }
  },
  methods: {
    logout () {
      this.$confirm('确认退出吗?', '退出提示', {
        confirmButtonText: '确定',
        cancelButtonText: '取消',
        type: 'warning'
      }).then(() => { // 点击确认执行 resolve 函数
        // 1. 删除本地存储中的 Token 身份标识
        window.localStorage.removeItem('token')
        // 2. 跳转到登陆视图
        this.$router.push({
          name: 'login'
        })
        this.$message({
          type: 'success',
          message: '退出成功!'
        })
      }).catch(() => {
        // 点击取消的处理
      })
    }
  }
}
</script>

<style>
.container {
  height: 100%;
}

.header {
  background-color: #b3c0d1;
}

.aside {
  background-color: #d3dce6;
}

.main {
  background-color: #e9eef3;
  height: 100%;
}
.home-header {
  background-color: #b3c0d1;
}
.home-header h2, .home-header .loginout {
  height: 60px;
  line-height: 60px;
}
.home-header .loginout a{
  text-decoration: none;
}
.home-aside {
  background-color: #e9eef3;
}
.home-content {
  background-color: #ccc;
}
</style>
