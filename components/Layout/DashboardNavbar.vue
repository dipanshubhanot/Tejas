<template>
  <base-nav
    v-model="showMenu"
    class="navbar-absolute top-navbar"
    type="white"
    :transparent="true"
  >
    <div slot="brand" class="navbar-wrapper">
      <div
        class="navbar-toggle d-inline"
        :class="{ toggled: $sidebar.showSidebar }"
      >
        <button type="button" class="navbar-toggler" @click="toggleSidebar">
          <span class="navbar-toggler-bar bar1"></span>
          <span class="navbar-toggler-bar bar2"></span>
          <span class="navbar-toggler-bar bar3"></span>
        </button>
      </div>
      <a class="navbar-brand ml-xl-3 ml-5" href="#pablo"
        >{{ routeName }} | MNS Platforms</a
      >
    </div>

    <ul class="navbar-nav" :class="$rtl.isRTL ? 'mr-auto' : 'ml-auto'">
      <!-- <div class="search-bar input-group" @click="searchModalVisible = true">
        <button
          class="btn btn-link"
          id="search-button"
          data-toggle="modal"
          data-target="#searchModal"
        >
          <i class="tim-icons icon-zoom-split"></i>
        </button>
      </div>
      <modal
        :show.sync="searchModalVisible"
        class="modal-search"
        id="searchModal"
        :centered="false"
        :show-close="true"
      >
        <input
          slot="header"
          v-model="searchQuery"
          type="text"
          class="form-control"
          id="inlineFormInputGroup"
          placeholder="SEARCH"
        />
      </modal> -->
      <base-dropdown
        tag="li"
        :menu-on-right="!$rtl.isRTL"
        title-tag="a"
        title-classes="nav-link"
        class="nav-item"
      >
        <template slot="title">
          <!-- <div class="notification d-none d-lg-block d-xl-block"></div> -->
          <i class="tim-icons icon-cart"></i> &nbsp; My Cart &nbsp;<badge type="primary">{{data.items.length}}</badge>

        </template>
        <li v-for="(item, index) in data.items" :key="index" class="nav-link">
          <div>
            <img :src="item.img" class="img-circle img-responsive">
          </div>
          <a href="#" class="nav-item dropdown-item">{{ item.name }}</a>
        </li>

        <div class="dropdown-divider"></div>
        <li class="nav-link">
          <a href="#" class="nav-item dropdown-item">Check out</a>
        </li>
      </base-dropdown>
      <!-- <base-dropdown
        tag="li"
        :menu-on-right="!$rtl.isRTL"
        title-tag="a"
        class="nav-item"
        title-classes="nav-link"
        menu-classes="dropdown-navbar"
      >
        <template
          slot="title"
        >
          <div class="photo"><i class="fas fa-user-circle"></i></div>
          <b class="caret d-none d-lg-block d-xl-block"></b>
          <p class="d-lg-none">My Account</p>
        </template>
        <li class="nav-link">
          <a href="#" class="nav-item dropdown-item"> <i class="fas fa-user"></i> Profile</a>
        </li>
        <li class="nav-link">
          <a href="#" class="nav-item dropdown-item"><i class="fas fa-history"></i>Order History</a>
        </li>
        <li class="nav-link">
          <a href="#" class="nav-item dropdown-item"><i class="fas fa-tools"></i>Settings</a>
        </li>
        <div class="dropdown-divider"></div>
        <li class="nav-link">
          <a href="#" class="nav-item dropdown-item"><i class="fas fa-sign-out-alt"></i>Log out</a>
        </li>
      </base-dropdown> -->
    </ul>
  </base-nav>
</template>
<script>
import { CollapseTransition } from "vue2-transitions";
import { BaseNav, Modal, Badge } from "@/components";

export default {
  components: {
    CollapseTransition,
    BaseNav,
    Modal,
    Badge
  },
  props: {
    data: {
      type: Object,
    },
  },
  computed: {
    routeName() {
      const { path } = this.$route;
      let parts = path.split("/");
      if (parts == ",") {
        return "Home";
      }
      return parts.map((p) => this.capitalizeFirstLetter(p)).join(" ");
    },
    isRTL() {
      return this.$rtl.isRTL;
    },
  },
  data() {
    return {
      activeNotifications: false,
      showMenu: false,
      searchModalVisible: false,
      searchQuery: "",
    };
  },
  methods: {
    capitalizeFirstLetter(string) {
      if (!string || typeof string !== "string") {
        return "";
      }
      return string.charAt(0).toUpperCase() + string.slice(1);
    },
    closeDropDown() {
      this.activeNotifications = false;
    },
    toggleSidebar() {
      this.$sidebar.displaySidebar(!this.$sidebar.showSidebar);
    },
    toggleMenu() {
      this.showMenu = !this.showMenu;
    },
  },
};
</script>
<style scoped>
.top-navbar {
  top: 0px;
}
</style>
