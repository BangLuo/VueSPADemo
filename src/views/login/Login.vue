<template>
  <div class="login-wrap">
    <el-form class="login-from" :model="ruleForm2" status-icon  ref="ruleForm2" label-width="100px">
      <el-form-item
      label="登录"
      prop="name">
        <el-input v-model.number="ruleForm2.username"></el-input>
      </el-form-item>
      <el-form-item
      label="密码"
      prop="pass">
        <el-input type="password" v-model="ruleForm2.password" auto-complete="off"></el-input>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="submitLoginForm" class="login-btn">提交</el-button>
      </el-form-item>
    </el-form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      ruleForm2: {
        username: '',
        password: ''
      }
    }
  },
  methods: {
    async submitLoginForm () {
      const {data: resData} = await this.$http.post('http://localhost:8888/api/private/v1/login', this.ruleForm2)
      const { data, meta: {status, msg}} = resData;
      console.log(resData);
      if (status === 200) {
        this.$message.success(msg);
        window.localStorage.setItem('token', data.token);
        this.$router.push({name: 'home'});
      } else {
        this.$message.warning(msg);
      }
    }
  }
}
</script>

<style>
.login-wrap {
  background-color: #324152;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.login-wrap .login-from {
  background-color: #fff;
  width: 400px;
  padding: 30px;
  border-radius: 5px;
}

.login-from {
  padding-top: 50px
}

.login-wrap .login-from .login-btn {
  width: 100px;
}

.el-form-item__label {
  text-align: center;
}
</style>
