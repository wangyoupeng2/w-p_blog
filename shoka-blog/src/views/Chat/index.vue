<template>
  <div class="home">
    <el-container height="100%">
      <el-aside width="100px">
        <Nav></Nav>
      </el-aside>
      <el-main>
        <router-view to="/chatHome"></router-view>
      </el-main>
    </el-container>
  </div>
</template>

<script>
import Nav from "@/components/ChatHome/Chat/Nav.vue";
import useStore from "@/store";
import EventBus from "@/eventBus.ts";
const { user, app } = useStore();

export default {
  name: "App",
  components: {
    Nav,
  },
  mounted() {
    if (!user.id || user.id === "") {
      app.setLoginFlag(true);
    }
    EventBus.on("refresh-chat", () => {
      if(window.location.pathname === "/chat/ChatHome") {
        window.location.reload(); // 触发页面刷新
      }
    });
  },
};
</script>

<style lang="scss" scoped>
::v-deep .el-container {
  height: 100%;
}

.home {
  width: 90vw;
  height: 90vh;
  background-color: rgb(39, 42, 55);
  border-radius: 15px;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
}
</style>
