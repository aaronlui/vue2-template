<template>
  <section class="app-main">
    <div class="app-scrollbar">
      <transition name="fade-transform" mode="out-in">
        <router-view :key="key" />
      </transition>
    </div>
  </section>
</template>

<script>
export default {
  name: 'AppMain',
  computed: {
    key() {
      return this.$route.path
    }
  }
}
</script>

<style lang="scss" scoped>
@import "~@/styles/mixin";
@import "~@/styles/variables";

.app-main {
  width: 100%;
  height: 100vh;
  padding-top: $navBarHeight;
  padding-left: $sideBarWidth;
  overflow: auto;
  transition: padding-left 0.28s;

  .app-scrollbar {
    @include scrollbar;

    height: 100%;
    overflow: auto;
  }
}
</style>

<style lang="scss">
// fix css style bug in open el-dialog
.el-popup-parent--hidden {
  .fixed-header {
    padding-right: 15px;
  }
}
</style>
