<template>
  <span class="vf-o-search-inline-form">
    <vf-a-input
      v-model="keyword"
      :placeholder="$t('elements.common.header.navSearch.placeholderText')"
      size="sm"
      :hide-details="!$vuefront.isAMP"
      @keypress.stop="handleKeyPress"
      trim
    />
  </span>
</template>
<script>
export default {
  data() {
    return {
      keyword: ""
    };
  },
  watch: {
    $route(to, from) {
      if (to.matched[0].path === "/search/:slug") {
        this.keyword = to.params.slug;
      } else {
        this.keyword = "";
      }
    }
  },
  watchQuery: true,
  methods: {
    handleKeyPress(e) {
      if (e.key === "Enter") {
        if (this.keyword !== "") {
          this.$router.push(`/search/${this.keyword}`);
        } else {
          this.$router.push("/search");
        }
      }
    },
    doSearch() {
      this.$router.push(`/search/${this.keyword}`);
    }
  },
  beforeMount() {
    if (
      this.$route.matched.length > 0 &&
      this.$route.matched[0].path === "/search/:slug"
    ) {
      this.keyword = this.$route.params.slug;
    }
  }
};
</script>
