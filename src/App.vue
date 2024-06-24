<template>
  <div id="app">
    <header class="header">
      <h1 class="logo">Жилфонд</h1>

      <span class="title">Пользователь</span>
    </header>

    <main class="main">
      <SideBar class="list" />

      <UserInfo class="info" />
    </main>
  </div>
</template>

<script>

import SideBar from '@/components/SideBar.vue'
import UserInfo from '@/components/UserInfo.vue'

export default {
  name: 'App',

  components: {
    SideBar,
    UserInfo
  },
}
</script>

<style lang="scss">
  @import '@/assets/style/fonts.scss';
  @import '@/assets/style/main.scss';
</style>

<style lang="scss" scoped>
#app {
  display: flex;
  flex-direction: column;
  padding: 50px 50px 58px;
  height: 100vh;
  box-sizing: border-box;
}

.header {
  display: flex;
  justify-content: space-between;
  margin-bottom: 26px;
  user-select: none;
}

.logo {
  margin: 0;
  font-size: 32px;
  font-weight: 700;
  line-height: 39.01px;
  text-align: left;
  color: #E31F24;
}

.title {
  font-size: 16px;
  font-weight: 400;
  line-height: 19.5px;
  text-align: left;
  color: #333333;

}

.main {
  display: flex;
  flex-direction: row;
  height: 100%;
  border-radius: 10px;
  box-shadow: 0px 0px 10px 0px #0000001A;
  background-color: #FDFDFD;
  overflow: hidden;
}

.list {
  min-width: 251px;
  border-right: 1px solid #E0E0E0;
}

.card {
  padding: 30px 30px 30px 21px;
}
</style>
