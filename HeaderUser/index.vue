<template>
  <div class="lea-user">
    <!-- 未登录 -->
    <div class="lea-user-operate" v-if="isOperate">
      <!-- 自定义操作内容 -->
      <slot name="oper" v-if="$slots.oper"></slot>
      <!-- 默认登录、注册 -->
      <div v-else class="oper-wrapper">
        <!-- 登录 -->
        <el-button class="login-btn" type="text" @click="login">
          登录
        </el-button>
        <!-- 注册 -->
        <el-button class="register-btn" type="text">
          <router-link :to="registerRoute">注册</router-link>
        </el-button>
      </div>
    </div>
    <!-- 已登录 -->
    <div v-else class="lea-user-info">
      <!-- 用户信息 -->
      <slot name="userinfo"></slot>
      <!-- 退出 -->
      <slot name="logout" v-if="$slots.logout"></slot>
      <el-button v-else type="text" class="logout-btn" @click="logout">退出</el-button>
    </div>
  </div>
</template>

<script>
export default {
  name: "lea-header-user",
  props: {
    // 是否显示非登录操作按钮
    isOperate: {
      type: Boolean,
      default: true,
    },

    // 注册路由
    registerRoute: {
      type: Object || String,
    },
  },
  methods: {
    login() {
      this.$emit("on-login");
    },

    logout() {
      this.$emit("on-logout");
    }
  },
};
</script>

<style lang="scss">
.lea-user {
  font-size: 16px;

  button,
  a {
    font-size: 16px;
  }


  .oper-wrapper,
  .lea-user-info {
    display: flex;
    align-items: center;
  }

  .logout-btn {
    margin-left: 25px;
  }
}
</style>