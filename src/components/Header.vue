<template>
  <div class="m-content">
    <h3>欢迎来到我的博客世界</h3>
    <div class="block">
      <div class="block">
        <el-avatar :size="50" :src="user.avatar"></el-avatar>
      </div>
      <div>{{user.username}}</div>
      <div class="maction">
        <span>
          <el-link @click="zhuye">主页</el-link>
        </span>
        <el-divider direction="vertical"></el-divider>
        <span>
          <el-link type="success" @click="fbbk">发表博客</el-link>
        </span>

        <el-divider direction="vertical"></el-divider>
        <span v-show="!hasLogin">
          <el-link type="primary" @click="login">登录</el-link>
        </span>
        <span v-show="hasLogin">
          <el-link type="danger" @click="logout">退出</el-link>
        </span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Header"
  , data () {
    return {
      user: {
        username: '请先登录',
        avatar: 'src/assets/logo.jpg'
      },
      hasLogin: false
    }
  },
  methods: {
    //退出操作
    logout () {
      const _this = this
      //首先调用后端logout接口(因该接口需要认证权限,所以需要传入token)
      //其次调用$store清除用户信息及token
      _this.$axios.get("/logout", {
        headers: {
          "Authorization": localStorage.getItem("token")
        }
      }).then(res => {
        _this.$store.commit("REMOVE_INFO")
        _this.$router.push("/login")
      })
    },
    login () { //跳转登录页面进行登录
      this.$router.push("/login")
    },
    fbbk () {
      this.$router.push("/blog/add")
    },
    zhuye () {
      this.$router.push("/blogs")
    }
  },
  //页面创建时即会调用,进而获取用户信息
  created () {
    if (this.$store.getters.getUser.username) {//如果username不为空
      this.user.username = this.$store.getters.getUser.username
      this.user.avatar = this.$store.getters.getUser.avatar
      //判断是登录状态还是非登录显示 退出按钮或者登录按钮
      this.hasLogin = true;
    }
  }
}
</script>

<style>
.m-content {
  max-width: 960px;
  margin: 0 auto;
  text-align: center;
}
.maction {
}
</style>