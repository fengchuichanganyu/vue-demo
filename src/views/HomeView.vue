<template>
  <div class="home">
    <el-container>
      <el-header
        ><el-row :gutter="20">
          <el-col :span="4"
            ><img src="../assets/logo.png" alt="" class="logo"
          /></el-col>
          <el-col :span="16"><h2>后台管理系统</h2></el-col>
          <el-col :span="4"
            ><el-button @click="logout" class="logout-btn"
              >退出登录</el-button
            ></el-col
          >
        </el-row></el-header
      >
      <el-container>
        <el-aside width="200px"
          ><el-menu
            active-text-color="#ffd04b"
            background-color="#545c64"
            class="el-menu-vertical-demo"
            :default-active="active"
            text-color="#fff"
            router
          >
            <!-- router是开启路由模式，开启之后能根据el-menu-item里面的idex跳转 -->
            <el-menu-item
              :index="item.path"
              v-for="item in list"
              :key="item.path"
            >
              <el-icon></el-icon>
              <span>{{ item.meta.title }}</span>
            </el-menu-item>
          </el-menu></el-aside
        >
        <el-main><router-view></router-view></el-main>
      </el-container>
    </el-container>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import { useRouter } from 'vue-router'
import { useRoute } from 'vue-router'
export default defineComponent({
  name: 'HomeView',

  setup() {
    const route = useRoute()
    const router = useRouter()
    const list = router.getRoutes().filter((v) => v.meta.isShow)
    // console.log(list)

    const logout = () => {
      localStorage.removeItem('token')
      router.push('/login')
    }
    return { router, list, active: route.path, logout }
  },
})
</script>

<style lang="scss" scoped>
.el-header {
  height: 80px;
  background-color: #67c13e;
  h2 {
    text-align: center;
    height: 80px;
    line-height: 80px;
  }
  .logout-btn {
    height: 80px;
    line-height: 80px;
  }
  .logo {
    height: 80px;
  }
}
.el-aside {
  .el-menu {
    height: calc(100vh - 80px);
  }
}
</style>
