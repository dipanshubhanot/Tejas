<template>
  <div class="wrapper" :class="{ 'nav-open': $sidebar.showSidebar }">
    <notifications></notifications>
    <side-bar
      :background-color="sidebarBackground"
      :short-title="$t('sidebar.shortTitle')"
      title="MNS Platforms"
    >
      <template slot-scope="props" slot="links">
        <sidebar-item
          :link="{
            name: $t('Home'),
            icon: 'tim-icons icon-double-right',
            path: '/',
          }"
        >
        </sidebar-item>
        <sidebar-item
          :link="{
            name: $t('Products'),
            icon: 'tim-icons icon-tag',
            path: '/products',
          }"
        >
        </sidebar-item>

        <sidebar-item
          :link="{
            name: $t('About Us'),
            icon: 'tim-icons icon-badge',
            path: '/user',
          }"
        >
        </sidebar-item>
      </template>
    </side-bar>
    <!--Share plugin (for demo purposes). You can remove it if don't plan on using it-->
    <!-- <sidebar-share :background-color.sync="sidebarBackground"> </sidebar-share> -->
    <div class="main-panel" :data="sidebarBackground">
      <dashboard-navbar
        :data="{
          items: [
            {
              name: 'Item1',
              img:
                'https://images.unsplash.com/photo-1513721223622-f3426ac30ee6?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=634&q=80',
              link: '#',
            },
          ],
        }"
      ></dashboard-navbar>
      <router-view name="header"></router-view>

      <div :class="{ content: !isFullScreenRoute }" @click="toggleSidebar">
        <zoom-center-transition :duration="200" mode="out-in">
          <!-- your content here -->
          <nuxt></nuxt>
        </zoom-center-transition>
      </div>
      <content-footer v-if="!isFullScreenRoute"></content-footer>
    </div>
  </div>
</template>
<script>
/* eslint-disable no-new */
import PerfectScrollbar from "perfect-scrollbar";
import "perfect-scrollbar/css/perfect-scrollbar.css";
import SidebarShare from "@/components/Layout/SidebarSharePlugin";
function hasElement(className) {
  return document.getElementsByClassName(className).length > 0;
}

function initScrollbar(className) {
  if (hasElement(className)) {
    new PerfectScrollbar(`.${className}`);
  } else {
    // try to init it later in case this component is loaded async
    setTimeout(() => {
      initScrollbar(className);
    }, 100);
  }
}

import DashboardNavbar from "@/components/Layout/DashboardNavbar.vue";
import ContentFooter from "@/components/Layout/ContentFooter.vue";
import DashboardContent from "@/components/Layout/Content.vue";
import { SlideYDownTransition, ZoomCenterTransition } from "vue2-transitions";

export default {
  components: {
    DashboardNavbar,
    ContentFooter,
    DashboardContent,
    SlideYDownTransition,
    ZoomCenterTransition,
    SidebarShare,
  },
  data() {
    return {
      sidebarBackground: "primary", //vue|blue|orange|green|red|primary
    };
  },
  computed: {
    isFullScreenRoute() {
      return this.$route.path === "/maps/full-screen";
    },
  },
  methods: {
    toggleSidebar() {
      if (this.$sidebar.showSidebar) {
        this.$sidebar.displaySidebar(false);
      }
    },
    initScrollbar() {
      let docClasses = document.body.classList;
      let isWindows = navigator.platform.startsWith("Win");
      if (isWindows) {
        // if we are on windows OS we activate the perfectScrollbar function
        initScrollbar("sidebar");
        initScrollbar("main-panel");
        initScrollbar("sidebar-wrapper");

        docClasses.add("perfect-scrollbar-on");
      } else {
        docClasses.add("perfect-scrollbar-off");
      }
    },
  },
  mounted() {
    this.initScrollbar();
  },
};
</script>
<style lang="scss">
$scaleSize: 0.95;
@keyframes zoomIn95 {
  from {
    opacity: 0;
    transform: scale3d($scaleSize, $scaleSize, $scaleSize);
  }
  to {
    opacity: 1;
  }
}

.main-panel .zoomIn {
  animation-name: zoomIn95;
}

@keyframes zoomOut95 {
  from {
    opacity: 1;
  }
  to {
    opacity: 0;
    transform: scale3d($scaleSize, $scaleSize, $scaleSize);
  }
}

.main-panel .zoomOut {
  animation-name: zoomOut95;
}
</style>
