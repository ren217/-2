<template>
  <el-container class="index">
    <el-aside width="200px" class="left">
      <!-- 左侧导航 -->
      <!-- 
        background-color 背景颜色
        text-color  文字颜色
        active-text-color  选中的那一个颜色
        unique-opened  只保持一个打开
        router 开启路由模式
       -->
      <el-menu default-active="2" class="el-menu-vertical-demo" background-color="rgb(21,23,31)" text-color="#fff"
        router unique-opened active-text-color="#ffd04b">
        <!-- 首页 -->
        <el-menu-item index="/">
          <i class="el-icon-s-shop"></i>
          <span>首页</span>
        </el-menu-item>
        <div v-for="item in userInfo.menus" :key="item.id">
          <!-- 目录 -->
          <el-submenu :index="item.id+''" v-if="item.children">
            <template slot="title">
              <i :class="item.icon"></i>
              <span>{{item.title}}</span>
            </template>
            <el-menu-item-group>
              <el-menu-item v-for="i in item.children" :key="i.id" :index="i.url">
                <span>{{i.title}}</span>
              </el-menu-item>
            </el-menu-item-group>
          </el-submenu>
          <!-- 菜单 -->
          <el-menu-item :index="item.url" v-else>
            <span>{{item.title}}</span>
          </el-menu-item>
        </div>


      </el-menu>
    </el-aside>
    <el-container>
      <el-header class="header">
        <div>
          <span>{{userInfo.username}}</span>
          <el-button @click="logOut">退出</el-button>
        </div>
      </el-header>
      <el-main>
        <el-breadcrumb separator-class="el-icon-arrow-right">
          <el-breadcrumb-item :to="{ path: '/' }">首页</el-breadcrumb-item>
          <el-breadcrumb-item>{{ $route.name }}</el-breadcrumb-item>
        </el-breadcrumb>
        <!-- 二级路由出口 -->
        <router-view class="erji"></router-view>
      </el-main>
    </el-container>
  </el-container>
</template>
<script>
  import {
    mapGetters,
    mapActions
  } from "vuex";
  export default {
    props: [],
    components: {},
    data() {
      return {};
    },
    computed: {
      ...mapGetters({
        userInfo: "userInfo"
      }),
    },
    methods: {
      ...mapActions({
        reqUserInfoAction: "reqUserInfoAction"
      }),
      logOut(){
        // 清空状态层的userinfo
        this.reqUserInfoAction({})
        // 跳到登录页
        this.$router.push("/login")
      }
    },
    mounted() {},
  };

</script>
<style scoped>
  .index {
    height: 100vh;
  }

  .left {
    height: 100vh;
    background-color: rgb(21, 23, 31);
  }

  .header {
    height: 100px;
    background: rgb(181, 194, 211);
  }

  .erji {
    padding-top: 20px;
  }
  .header div{
    float: right;
  }

</style>
