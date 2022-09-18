<template>
  <div class="home-my-feed"><RwvArticleList type="history" /></div>
</template>

<script>
import RwvArticleList from "@/components/ArticleList";

export default {
  name: "rwv-home-my-history",
  components: {
    RwvArticleList
  }
};
</script>
