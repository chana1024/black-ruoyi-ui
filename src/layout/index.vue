<template>
  <div class="fix-header fix-sidebar card-no-border">
    <!-- Preloader - style you can find in spinners.css -->
<!--    <div class="preloader">
      <svg class="circular" viewBox="25 25 50 50">
        <circle class="path" cx="50" cy="50" r="20" fill="none" stroke-width="2" stroke-miterlimit="10" /> </svg>
    </div>-->
    <!-- Main wrapper - style you can find in pages.scss -->
    <div id="main-wrapper">
      <topbar></topbar>
      <left-sidebar></left-sidebar>
      <app-main></app-main>
    </div>
  </div>
</template>

<script>
import { Topbar, LeftSidebar, AppMain } from './components'
import ResizeMixin from './mixin/ResizeHandler'
import { mapState } from 'vuex'

export default {
  name: 'Layout',
  components: {
    Topbar,
    LeftSidebar,
    AppMain
  },
  mixins: [ResizeMixin],
  created: function(){
      $(function () {
        $('#sidebarnav').metisMenu();
          // ==============================================================
          // Theme options
          // ==============================================================
        $(".sidebartoggler").on('click', function () {
              if ($("body").hasClass("mini-sidebar")) {
                $("body").trigger("resize");
                $(".scroll-sidebar, .slimScrollDiv").css("overflow", "hidden").parent().css("overflow", "visible");
                $("body").removeClass("mini-sidebar");
                $('.navbar-brand span').show();
                //$(".sidebartoggler i").addClass("ti-menu");
              }
              else {
                $("body").trigger("resize");
                $(".scroll-sidebar, .slimScrollDiv").css("overflow-x", "visible").parent().css("overflow", "visible");
                $("body").addClass("mini-sidebar");
                $('.navbar-brand span').hide();
                //$(".sidebartoggler i").removeClass("ti-menu");
              }
            });
        $('.scroll-sidebar').slimScroll({
          position: 'left'
          , size: "5px"
          , height: '100%'
          , color: '#dcdcdc'
        });
        $('.message-center').slimScroll({
          position: 'right'
          , size: "5px"

          , color: '#dcdcdc'
        });


        $('.aboutscroll').slimScroll({
          position: 'right'
          , size: "5px"
          , height: '80'
          , color: '#dcdcdc'
        });
        $('.message-scroll').slimScroll({
          position: 'right'
          , size: "5px"
          , height: '570'
          , color: '#dcdcdc'
        });
        $('.chat-box').slimScroll({
          position: 'right'
          , size: "5px"
          , height: '470'
          , color: '#dcdcdc'
        });

        $('.slimscrollright').slimScroll({
          height: '100%'
          , position: 'right'
          , size: "5px"
          , color: '#dcdcdc'
        });
        $(".search-box a, .search-box .app-search .srh-btn").on('click', function () {
          $(".app-search").toggle(200);
        });
        $('[data-toggle="tooltip"]').tooltip()
        $('[data-toggle="popover"]').popover()

        // Right sidebar options
        // ==============================================================
        $(".right-side-toggle").click(function () {
          $(".right-sidebar").slideDown(50);
          $(".right-sidebar").toggleClass("shw-rside");

        });

      });

  },
  computed: {
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
  },
  methods: {
    handleClickOutside() {
      this.$store.dispatch('app/closeSideBar', { withoutAnimation: false })
    },
    async logout() {
      this.$confirm('确定注销并退出系统吗？', '提示', {
        confirmButtonText: '确定',
        cancelButtonText: '取消',
        type: 'warning'
      }).then(() => {
        this.$store.dispatch('LogOut').then(() => {
          location.reload()
        })
      })
    }
  }
}
</script>

<style lang="scss" scoped>
  @import "~@/assets/styles/mixin.scss";
  @import "~@/assets/styles/variables.scss";

  @import "/assets/plugins/bootstrap/css/bootstrap.min.css";
  @import "/css/style.css";
  @import "/css/colors/green-dark.css";

  aside {
    background: #eef1f6;
    padding: 70px 0px;
    margin-bottom: 0px;
    border-radius: 2px;
    display: block;
    line-height: 18px;
    font-size: 20px;
    font-family: -apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,Oxygen,Ubuntu,Cantarell,"Fira Sans","Droid Sans","Helvetica Neue",sans-serif;
    color: #2c3e50;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }
 /* .app-wrapper {
    @include clearfix;
    position: relative;
    height: 100%;
    width: 100%;

    &.mobile.openSidebar {
      position: fixed;
      top: 0;
    }
  }

  .drawer-bg {
    background: #000;
    opacity: 0.3;
    width: 100%;
    top: 0;
    height: 100%;
    position: absolute;
    z-index: 999;
  }

  .fixed-header {
    position: fixed;
    top: 0;
    right: 0;
    z-index: 9;
    width: calc(100% - #{$sideBarWidth});
    transition: width 0.28s;
  }

  .hideSidebar .fixed-header {
    width: calc(100% - 54px)
  }

  .mobile .fixed-header {
    width: 100%;
  }*/
</style>
