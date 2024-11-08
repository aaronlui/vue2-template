<template>
  <div class="navbar">
    <div class="logo-wrapper">
      <h1 class="title">{{ title }}</h1>
    </div>
    <div class="content">

      <hamburger :is-active="sidebar.opened" class="hamburger-container" @toggleClick="toggleSideBar" />

      <breadcrumb class="breadcrumb-container" />

      <div class="right-menu">
        <el-dropdown class="avatar-container" trigger="click">
          <div class="avatar-wrapper">
            <img :src="avatar + '?imageView2/1/w/80/h/80'" class="user-avatar">
            <i class="el-icon-caret-bottom" />
          </div>
          <el-dropdown-menu slot="dropdown" class="user-dropdown">
            <router-link to="/">
              <el-dropdown-item>
                Home
              </el-dropdown-item>
            </router-link>
            <a target="_blank" href="https://github.com/PanJiaChen/vue-admin-template/">
              <el-dropdown-item>Github</el-dropdown-item>
            </a>
            <a target="_blank" href="https://panjiachen.github.io/vue-element-admin-site/#/">
              <el-dropdown-item>Docs</el-dropdown-item>
            </a>
            <el-dropdown-item divided @click.native="logout">
              <span style="display: block;">Log Out</span>
            </el-dropdown-item>
          </el-dropdown-menu>
        </el-dropdown>
      </div>
    </div>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
import Breadcrumb from '@/components/Breadcrumb'
import Hamburger from '@/components/Hamburger'
import { title } from '@/settings'

export default {
  components: {
    Breadcrumb,
    Hamburger
  },
  computed: {
    title() {
      return title
    },
    ...mapGetters([
      'sidebar',
      'avatar'
    ])
  },
  methods: {
    toggleSideBar() {
      this.$store.dispatch('app/toggleSideBar')
    },
    async logout() {
      await this.$store.dispatch('user/logout')
      this.$router.push(`/login?redirect=${this.$route.fullPath}`)
    }
  }
}
</script>

<style lang="scss" scoped>
@import "~@/styles/variables";

.navbar {
  display: flex;
  height: $navBarHeight;
  padding: 0 20px;
  background: #fff;
  box-shadow: 0 1px 4px rgb(0 21 41 / 8%);

  .logo-wrapper {
    .title {
      font-size: 20px;
      line-height: $navBarHeight;
      color: #303133;
    }
  }

  .content {
    display: flex;
    flex: 1;
    align-items: center;

    .hamburger-container {
      cursor: pointer;
      transition: background 0.3s;
      -webkit-tap-highlight-color: transparent;

      &:hover {
        background: rgb(0 0 0 / 2.5%);
      }
    }

    .breadcrumb-container {
      flex: 1;
    }

    .right-menu {
      height: 100%;

      &:focus {
        outline: none;
      }

      .right-menu-item {
        display: inline-block;
        height: 100%;
        padding: 0 8px;
        font-size: 18px;
        color: #5a5e66;
        vertical-align: text-bottom;

        &.hover-effect {
          cursor: pointer;
          transition: background 0.3s;

          &:hover {
            background: rgb(0 0 0 / 2.5%);
          }
        }
      }

      .avatar-container {
        margin-right: 30px;

        .avatar-wrapper {
          position: relative;
          margin-top: 5px;

          .user-avatar {
            width: 40px;
            height: 40px;
            cursor: pointer;
            border-radius: 10px;
          }

          .el-icon-caret-bottom {
            position: absolute;
            top: 25px;
            right: -20px;
            font-size: 12px;
            cursor: pointer;
          }
        }
      }
    }
  }
}
</style>
