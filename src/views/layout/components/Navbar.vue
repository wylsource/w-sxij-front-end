<template>
  <el-menu class="navbar"
    background-color="#485057"
    text-color="#fff"
    active-text-color="#ffd04b"
    mode="horizontal">
    <el-menu-item class="w-logo" index="0">
      <img src="../../../assets/logo_images/w-sxij-backstageSupporter.png" alt="w-logo" class="w-logo-img">
    </el-menu-item>
    
      <hamburger class="hamburger-container" :toggleClick="toggleSideBar" :isActive="sidebar.opened"></hamburger>
    <el-menu-item index="1">处理中心</el-menu-item>
      <el-submenu index="2">
        <template slot="title">我的工作台</template>
        <el-menu-item index="2-1">选项1</el-menu-item>
        <el-menu-item index="2-2">选项2</el-menu-item>
        <el-menu-item index="2-3">选项3</el-menu-item>
      </el-submenu>
      <el-menu-item index="3">
        订单管理
      </el-menu-item>
    <el-dropdown class="avatar-container" trigger="click">
      <div class="avatar-wrapper">
        <img class="user-avatar" 
        src="/src/assets/user_images/武玉龙.png"
        >
        <!-- :src="avatar+'?imageView2/1/w/80/h/80'" -->
        <i class="el-icon-caret-bottom"></i>
      </div>
      <el-dropdown-menu class="user-dropdown" slot="dropdown">
        <router-link class="inlineBlock" to="/">
          <el-dropdown-item>
            Home
          </el-dropdown-item>
        </router-link>
        <el-dropdown-item divided>
          <span @click="logout" style="display:block;">LogOut</span>
        </el-dropdown-item>
      </el-dropdown-menu>
    </el-dropdown>
  </el-menu>
  
</template>

<script>
import { mapGetters } from 'vuex'
// import Breadcrumb from '@/components/Breadcrumb'
import Hamburger from '@/components/Hamburger'

export default {
  components: {
    // Breadcrumb,
    Hamburger
  },
  computed: {
    ...mapGetters([
      'sidebar',
      'avatar'
    ])
  },
  methods: {
    toggleSideBar() {
      this.$store.dispatch('ToggleSideBar')
    },
    logout() {
      this.$store.dispatch('LogOut').then(() => {
        location.reload() // 为了重新实例化vue-router对象 避免bug
      })
    }
  }
}
</script>

<style rel="stylesheet/scss" lang="scss" scoped>
.navbar {
  height: 60px;
  line-height: 50px;
  position: fixed;
  width: 100%;
  z-index: 3;
  padding-top: 0px;
  border-radius: 0px !important;
  .w-logo {
    text-align: left;
    font-size: 23px;
    padding-left: 10px;
    padding-right: 50px;
  }
  .w-logo-img {
    text-align: center;
    align-self: center;
    padding-left: 0px;
    width: 140px;
    height: 50px;
  }
  .hamburger-container {
    line-height: 58px;
    height: 50px;
    float: left;
    padding-top: 10px;
    // padding: 0 10px;
  }
  .screenfull {
    position: absolute;
    right: 90px;
    top: 16px;
    color: red;
  }
  .avatar-container {
    height: 50px;
    display: inline-block;
    position: absolute;
    right: 35px;
    .avatar-wrapper {
      cursor: pointer;
      margin-top: 10px;
      position: relative;
      .user-avatar {
        width: 40px;
        height: 40px;
        border-radius: 10px;
      }
      .el-icon-caret-bottom {
        position: absolute;
        right: -20px;
        top: 25px;
        font-size: 12px;
      }
    }
  }
}
</style>

