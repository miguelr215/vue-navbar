<template>
  <div class="container my-3">
    <form action="">
      <div class="mb-3">
        <label for="" class="form-label"> Page Title </label>

        <!-- method 1 of getting input value -->
        <!-- <input type="text" class="form-control" :value="pageTitle" @input="(e) => pageTitle = e.target.value" required> -->
        <!-- method 2 of getting input value -->

        <input type="text" class="form-control" v-model="pageTitle" required />
      </div>

      <div class="mb-3">
        <label for="" class="form-label">Link Text</label>
        <input type="text" class="form-control" v-model="linkText" />
      </div>

      <div class="mb-3">
        <label for="" class="form-label">Link URL</label>
        <input type="text" class="form-control" v-model="linkUrl" />
      </div>

      <div class="mb-3">
        <div class="form-check">
          <input type="checkbox" class="form-check-input" v-model="published" />
          <label for="gridCheck1" class="form-check-label">Published</label>
        </div>
      </div>

      <div class="mb-3">
        <label for="" class="form-label"> Content </label>
        <textarea type="text" class="form-control" rows="5" v-model="content" required></textarea>
      </div>

      <div class="mb-3">
        <!-- <button class="btn btn-primary" @click.prevent="pageCreated({pageTitle, content})">Create Page</button> -->

        <button class="btn btn-primary" @click.prevent="submitForm" :disabled="isFormInvalid">
          Create Page
        </button>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  props: ['pageCreated'],
  computed: {
    isFormInvalid() {
      return !this.pageTitle || !this.content || !this.linkText || !this.linkUrl;
    },
  },
  data() {
    return {
      pageTitle: '',
      content: '',
      linkText: '',
      linkUrl: '',
      published: true,
    };
  },
  methods: {
    submitForm() {
      if (!this.pageTitle || !this.content || !this.linkText || !this.linkUrl) {
        alert('Please fill all the fields');

        return;
      } else {
        this.pageCreated({
          title: this.pageTitle,
          content: this.content,
          link: {
            text: this.linkText,
            url: this.linkUrl,
          },
          published: this.published,
        });

        this.pageTitle = '';
        this.content = '';
        this.linkText = '';
        this.linkUrl = '';
        this.published = true;
      }
    },
  },
  watch: {
    pageTitle(newTitle, oldTitle) {
      if (this.linkText === oldTitle) {
        this.linkText = newTitle;
      }
    },
  },
};
</script>
