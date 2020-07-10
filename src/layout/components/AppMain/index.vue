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
       <div :class="{hasTagsView:needTagsView}">
          <div :class="{'fixed-header':fixedHeader}">
            <tags-view v-if="needTagsView" />
          </div>
         <!--<app-header></app-header>-->
         <transition name="fade-transform" mode="out-in">
           &lt;!&ndash;<keep-alive :include="cachedViews">&ndash;&gt;
           <router-view :key="key">{{key}}</router-view>
           &lt;!&ndash;</keep-alive>&ndash;&gt;
         </transition>
        </div>
        <app-footer></app-footer>
      </div>
  </div>

</template>

<script>
import AppHeader from './AppHeader'
import AppFooter from './AppFooter'
import { mapState } from 'vuex'
import {default as TagsView} from '../TagsView/index.vue'
import ResizeMixin from '../../mixin/ResizeHandler'

export default {
  components: { AppHeader, AppFooter ,TagsView},
  mixins: [ResizeMixin],
  computed: {
    cachedViews() {
      return this.$store.state.tagsView.cachedViews
    },
    key() {
      return this.$route.path;
    },
    ...mapState({
        sidebar: state => state.app.sidebar,
        device: state => state.app.device,
        showSettings: state => state.settings.showSettings,
        needTagsView: state => state.settings.tagsView,
        fixedHeader: state => state.settings.fixedHeader
      }),
    classObj() {
        return {
          hideSidebar: !this.sidebar.opened,
          openSidebar: this.sidebar.opened,
          withoutAnimation: this.sidebar.withoutAnimation,
          mobile: this.device === 'mobile'
        }
      }
    }
}
</script>

<style lang="scss" scoped>

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
