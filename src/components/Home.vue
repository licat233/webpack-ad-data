<template>
  <el-container class="home-container">
    <!-- 头部区域 -->
    <el-header>
      <div>
        <div>
          <img src="../assets/images/avatar.jpg" alt="享购广告数据监控系统" />
        </div>
        <span>享购广告数据监控系统</span>
      </div>
      <el-button size="mini" type="primary" @click="logout()">退出</el-button>
    </el-header>
    <!--页面主体区域-->
    <el-container>
      <!--侧边栏-->
      <!-- <el-aside> -->
        <el-menu
          default-active="1-4-1"
          class="el-menu-vertical-aside"
          @open="handleOpen"
          @close="handleClose"
          :collapse="isCollapse"
        >
          <el-menu-item index="1" @click="mstatus()">
              <i v-bind:class="[ isCollapse ? openMenu : closeMenu ]"></i>
              <span slot="title">{{Menuname}}</span>
          </el-menu-item>
          <el-menu-item index="2">
            <i class="el-icon-pie-chart"></i>
            <span slot="title">成本</span>
          </el-menu-item>
          <el-menu-item index="3">
            <i class="el-icon-bank-card"></i>
            <span slot="title">消耗</span>
          </el-menu-item>
          <el-menu-item index="4">
            <i class="el-icon-user"></i>
            <span slot="title">加粉</span>
          </el-menu-item>
        </el-menu>
      <!-- </el-aside> -->
      <!-- 右侧内容主体 -->
      <el-main>
        <ve-chats></ve-chats>
      </el-main>
    </el-container>
  </el-container>
</template>

<script>
export default {
  created() {
    this.getMenuList()
  },
  data() {
    return {
      isCollapse: true,
      openMenu: 'el-icon-arrow-right',
      closeMenu: 'el-icon-arrow-left',
      Menuname: '打开'
    }
  },
  methods: {
    logout () {
      window.sessionStorage.clear()
      this.$router.push('/login')
    },
    handleOpen(key, keyPath) {
      console.log(key, keyPath)
    },
    handleClose(key, keyPath) {
      console.log(key, keyPath)
    },
    mstatus () {
      this.isCollapse = !this.isCollapse
      this.isCollapse ? this.Menuname = '打开' : this.Menuname = '收起'
    },
    async getMenuList() {
      const { data: res } = await this.$http.get('menus')
      console.log(res)
    }
  },
  components: {
    've-chats': () => import('./Charts')
  }
}
</script>

<style lang="less" scoped>
.home-container {
  height: 100%;
}
.el-header {
  background-image: linear-gradient(
    to Right,
    #1e90ff,
    #409eff,
    #53a8ff,
    #66b1ff,
    #79bbff,
    #b3d8ff,
    #c6e2ff
  );
  box-shadow: 0px 0px 8px 1px #DCDCDC;
  // background-color: #1E90FF;
  display: flex;
  justify-content: space-between;
  padding-left: 5px;
  align-items: center;
  color: #ffffff;
  font-size: 20px;
  > div {
    display: flex;
    align-items: center;
    div {
      background-color: white;
      border-radius: 50%;
      padding: 3px;
      width: 40px;
      height: 40px;
      border: 1px solid #eee;
      box-shadow: 0px 0px 5px 1px #0000cd;
      img {
        width: 100%;
        height: 100%;
        border-radius: 50%;
      }
    }
    span {
      margin-left: 15px;
    }
  }
}
// .el-aside {
//   width:50px;
// }
.el-menu {
  height: 224px;
  margin-top: 20px;
  box-shadow: 0px 0px 8px 1px #DCDCDC;
  // position: fixed;
}
.el-menu-vertical-aside:not(.el-menu--collapse) {
  width: 150px;
  box-shadow: 0px 0px 8px 1px #DCDCDC;
  margin-top: 20px;
}
.el-main {
  background-color: #ffffff;
  margin-top: 20px;
  max-width: 1200px;
  margin: 0 auto;
}
</style>
