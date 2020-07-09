<template >
    <li v-if="item.meta&&!item.hidden">
      <template v-if="item.children">
        <a class=" has-arrow waves-effect waves-dark" href="#" aria-expanded="false"><i class="mdi mdi-gauge"></i><span class="hide-menu">{{item.meta.title}} </span></a>
        <ul aria-expanded="true" class="collapse">
          <!--<li><router-link :to="item.path"></router-link></li>-->
          <sidebar-item
            v-for="child in item.children"
            :key="child.path"
            :is-nest="true"
            :item="child"
            :base-path="resolvePath(item.path)"
            class="nest-menu"
          />
        </ul>
      </template>
      <template v-else>
        <app-link :to="resolvePath(item.path)">
          <item :icon="item.meta.icon" :title="item.meta.title" />
        </app-link>
      </template>
    </li>
</template>

<script>
import path from 'path'
import { isExternal } from '@/utils/validate'
import FixiOSBug from './FixiOSBug'
import AppLink from './Link'
import Item from './Item'

export default {
  name: 'SidebarItem',
  components: {AppLink,Item},
  mixins: [FixiOSBug],
  props: {
    // route object
    item: {
      type: Object,
      required: true
    },
    isNest: {
      type: Boolean,
      default: false
    },
    basePath: {
      type: String,
      default: ''
    }
  },
  data() {
    this.onlyOneChild = null
    return {}
  },
  methods: {
    hasOneShowingChild(children = [], parent) {
      const showingChildren = children.filter(item => {
        if (item.hidden) {
          return false
        } else {
          // Temp set(will be used if only has one showing child)
          this.onlyOneChild = item
          return true
        }
      })

      // When there is only one child router, the child router is displayed by default
      if (showingChildren.length === 1) {
        return true
      }

      // Show parent if there are no child router to display
      if (showingChildren.length === 0) {
        this.onlyOneChild = { ... parent, path: '', noShowingChildren: true }
        return true
      }

      return false
    },
    resolvePath(routePath) {
      if (isExternal(routePath)) {
        return routePath
      }
      if (isExternal(this.basePath)) {
        return this.basePath
      }
      return path.resolve(this.basePath, routePath)
    }
  }
}
</script>
<style lang="scss" scoped>
</style>
