<template>
  <aside class="left-sidebar">
    <!-- Sidebar scroll-->
    <div class="scroll-sidebar">
      <!-- User profile -->
      <div class="user-profile" style="background: url(../assets/images/background/user-info.jpg) no-repeat;">
        <!-- User profile image -->
        <div class="profile-img"> <img src="@/assets/images/users/profile.png" alt="user" /> </div>
        <!-- User profile text-->
        <div class="profile-text"> <a href="#" class="dropdown-toggle u-dropdown" data-toggle="dropdown" role="button" aria-haspopup="true" aria-expanded="true">Markarn Doe</a>
          <div class="dropdown-menu animated flipInY"> <a href="#" class="dropdown-item"><i class="ti-user"></i> My Profile</a> <a href="#" class="dropdown-item"><i class="ti-wallet"></i> My Balance</a> <a href="#" class="dropdown-item"><i class="ti-email"></i> Inbox</a>
            <div class="dropdown-divider"></div> <a href="#" class="dropdown-item"><i class="ti-settings"></i> Account Setting</a>
            <div class="dropdown-divider"></div> <a href="login.html" class="dropdown-item"><i class="fa fa-power-off"></i> Logout</a> </div>
        </div>
      </div>
      <!-- End User profile text-->
      <!-- Sidebar navigation-->
      <nav class="sidebar-nav">
        <ul id="sidebarnav">
          <sidebar-item
            v-for="(route, index) in permission_routes"
            :key="route.path  + index"
            :item="route"
            :base-path="route.path"
          />
        </ul>
      </nav>
      <!-- End Sidebar navigation -->
    </div>
    <!-- End Sidebar scroll-->
    <!-- Bottom points-->
    <div class="sidebar-footer">
      <!-- item--><a href="" class="link" data-toggle="tooltip" title="Settings"><i class="ti-settings"></i></a>
      <!-- item--><a href="" class="link" data-toggle="tooltip" title="Email"><i class="mdi mdi-gmail"></i></a>
      <!-- item--><a @click="logout" href="javascript:void(0)" class="link" data-toggle="tooltip" title="Logout"><i class="mdi mdi-power"></i></a>
    </div>
    <!-- End Bottom points-->
  </aside>
</template>

<script type="text/ecmascript-6">
import { mapGetters, mapState } from "vuex";
import SidebarItem from './SidebarItem'
export default {
  components: {SidebarItem},
  computed: {
    ...mapState(["settings"]),
    ...mapGetters(["permission_routes", "sidebar"]),
    activeMenu() {
      const route = this.$route;
      const { meta, path } = route;
      // if set path, the sidebar will highlight the path you set
      if (meta.activeMenu) {
        return meta.activeMenu;
      }
      return path;
    },
    showLogo() {
      return this.$store.state.settings.sidebarLogo;
    },
    variables() {
      return variables;
    },
    isCollapse() {
      return !this.sidebar.opened;
    },
  },
  methods:{
    logout:function () {
      this.$parent.logout();
    }
  }
}
</script>

<style lang="scss" rel="stylesheet/stylus">
  .svg-icon {
    margin-right: 16px;
  }
</style>
