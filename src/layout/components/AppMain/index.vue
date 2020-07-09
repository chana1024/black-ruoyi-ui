<template>
<!--  <section class="app-main">
    <transition name="fade-transform" mode="out-in">
      <keep-alive :include="cachedViews">
        <router-view :key="key" />
      </keep-alive>
    </transition>
  </section>-->
  <div class="page-wrapper app-main">
    <div class="container-fluid">
      <!--<app-header></app-header>-->
      <transition name="fade-transform" mode="out-in">
        &lt;!&ndash;<keep-alive :include="cachedViews">&ndash;&gt;
        <router-view :key="key">{{key}}</router-view>
        &lt;!&ndash;</keep-alive>&ndash;&gt;
      </transition>
    </div>
    <app-footer></app-footer>
  </div>
</template>

<script>
import AppHeader from './AppHeader'
import AppFooter from './AppFooter'
export default {
  components: { AppHeader, AppFooter },
  computed: {
    cachedViews() {
      return this.$store.state.tagsView.cachedViews
    },
    key() {
      console.info(this.$route.path);
      return this.$route.path;

    }
  }
}
</script>

<style lang="scss" scoped>
/*  @import "/assets/plugins/bootstrap/css/bootstrap.min.css";
  @import "/css/style.css";
  @import "/css/colors/green-dark.css";*/

  .app-main {
    /* 50= navbar  50  */
    min-height: calc(100vh - 50px) !important;
    position: relative;
    overflow: hidden;
  }
  .fixed-header+.app-main {
    padding-top: 50px;
  }

  .hasTagsView {
    .app-main {
      /* 84 = navbar + tags-view = 50 + 34 */
      min-height: calc(100vh - 84px);
    }

    .fixed-header+.app-main {
      padding-top: 84px;
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
