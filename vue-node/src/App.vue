<template>
  <div id="app">
      <div>
        <el-input class="form-control" id="inputEmail3" placeholder="请输入账号" v-model="account">
          <template slot="prepend">用户名:</template>
        </el-input>
      </div>
      <div>
        <el-input class="form-control" id="inputPassword3" type="password" placeholder="请输入密码" v-model="password">
          <template slot="prepend">用户名:</template>
        </el-input>
      </div>
      <div style="margin: 20px 0">
        <el-button type="primary" plain class="btn btn-default" @click="login">登录</el-button>
      </div>
  </div>
</template>

<script>



export default {
  data () {
    return {
      account:'',
      password:''
    }
  },
  name: 'app',
  components: {
    
  },
  methods:{
      login() {
        // 获取已有账号密码
        this.$http.get('/api/login/getAccount')
          .then((response) => {
            // 响应成功回调
            console.log(response)
            let params = { 
              account : this.account,
              password : this.password
            };
            // 创建一个账号密码
            return this.$http.post('/api/login/createAccount',params);
          })
          .then((response) => {
            console.log(response)
          })
          .catch((reject) => {
            console.log(reject)
          });
        }
      }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
