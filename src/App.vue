<template>
  <header-navbar :pages="pages" :active-page="activePage"></header-navbar>
  <page-viewer v-if="pages.length > 0" :page="pages[activePage]"></page-viewer>
  <create-page :page-created="pageCreated"></create-page>
</template>

<script>
import PageViewer from './components/PageViewer.vue';
import HeaderNavbar from './components/HeaderNavbar.vue';
import CreatePage from './components/CreatePage.vue';

export default {
  components: {
    PageViewer,
    HeaderNavbar,
    CreatePage,
  },
  created() {
    this.getPages();

    this.$bus.$on('navbarLinkActivated', (index) => {
      this.activePage = index;
    });
  },
  data() {
    return {
      activePage: 0,
      pages: [],
    };
  },
  methods: {
    async getPages() {
      let res = await fetch('pages.json');
      let data = await res.json();

      this.pages = data;
    },
    pageCreated(pageOb) {
      console.log(pageOb);
      this.pages.push(pageOb);
    },
  },
};
</script>

<style></style>
