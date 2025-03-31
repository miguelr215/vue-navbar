<template>
  <header-navbar
    :pages="pages"
    :active-page="activePage"
    :nav-link-click="(index) => (activePage = index)"
  ></header-navbar>
  <page-viewer :page="pages[activePage]"></page-viewer>
</template>

<script>
import PageViewer from './components/PageViewer.vue';
import HeaderNavbar from './components/HeaderNavbar.vue';

export default {
  components: {
    PageViewer,
    HeaderNavbar,
  },
  data() {
    return {
      activePage: 0,
      pages: [
        {
          pageTitle: 'Home Page',
          content: 'this is the home page',
          link: { text: 'Home', url: 'home.html' },
        },
        {
          pageTitle: 'About Page',
          content: 'this is the about page',
          link: { text: 'About', url: 'about.html' },
        },
        {
          pageTitle: 'Contact Page',
          content: 'this is the contact page',
          link: { text: 'Contact', url: 'contact.html' },
        },
      ],
    };
  },
};
</script>

<style></style>
