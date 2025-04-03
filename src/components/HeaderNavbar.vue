<template>
  <nav :class="[`navbar-${theme}`, `bg-${theme}`, 'navbar', 'navbar-expand-lg']">
    <div class="container-fluid">
      <a class="navbar-brand" href="#">Navbar</a>
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarSupportedContent"
        aria-controls="navbarSupportedContent"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav me-auto mb-2 mb-lg-0">
          <li class="nav-item" v-for="(page, index) in publishedPages" :key="index">
            <navbar-link
              :page="page"
              :isActive="activePage === index"
              @click.prevent="navLinkClick(index)"
            ></navbar-link>
          </li>
        </ul>
      </div>
      <form class="d-flex">
        <button class="btn btn-primary" @click.prevent="changeTheme()">Toggle Dark Mode</button>
      </form>
    </div>
  </nav>
</template>

<script>
import NavbarLink from './NavbarLink.vue';

export default {
  components: { NavbarLink },
  created() {
    this.getThemeSetting();
  },
  computed: {
    publishedPages() {
      return this.pages.filter((page) => page.published);
    },
  },
  props: ['pages', 'activePage', 'navLinkClick'],
  data() {
    return {
      theme: 'light',
    };
  },
  // methods
  methods: {
    changeTheme() {
      this.theme = this.theme === 'light' ? 'dark' : 'light';
      this.storeThemeSetting();
    },
    storeThemeSetting() {
      localStorage.setItem('theme', this.theme);
    },
    getThemeSetting() {
      let theme = localStorage.getItem('theme');
      if (theme) {
        this.theme = theme;
      }
    },
  },
};
</script>

<style></style>
