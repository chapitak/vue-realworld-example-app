<template>
  <div class="article-page">
    <div class="banner">
      <div class="container">
        <h1>{{ article.title }}</h1>
      </div>
    </div>
    <div class="container">
      <div class="col-xs-12">이력유형: {{ article.revType }}</div>
      <hr />
      <div class="row article-content">
        <div class="col-xs-12">
          <div v-html="parseMarkdown(article.body)"></div>
        </div>
      </div>
      <hr />
    </div>
  </div>
</template>

<script>
import { mapGetters } from "vuex";
import marked from "marked";
import store from "@/store";
import { FETCH_ARTICLE_HISTORY } from "@/store/actions.type";

export default {
  name: "rwv-article",
  props: {
    id: {
      type: String,
      required: true
    }
  },
  components: {},
  beforeRouteEnter(to, from, next) {
    Promise.all([store.dispatch(FETCH_ARTICLE_HISTORY, to.params.id)]).then(
      () => {
        next();
      }
    );
  },
  computed: {
    ...mapGetters(["article", "currentUser"])
  },
  methods: {
    parseMarkdown(content) {
      return marked(content);
    }
  }
};
</script>
