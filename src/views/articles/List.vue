<template>
  <div class="col-md-9 left-col pull-right">
    <div class="panel article-body article-index">
      <div class="panel-body">
        <h1 class="all-articles">
          专栏文章
          <router-link v-if="auth" to="/articles/create" class="btn btn-primary pull-right">
            <i class="fa fa-paint-brush"></i>
            创作文章
          </router-link>
        </h1>

        <ul class="list-group">
          <li v-for="article in articles" class="list-group-item">
            <img :src="article.uavatar" class="avatar avatar-small">
            <router-link :to="`/articles/${article.articleId}/content`" class="title">
              {{ article.title }}
            </router-link>
            <span class="meta pull-right">
              <span class="timeago">{{ article.date | moment('from') }}</span>
            </span>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
  import { mapState } from 'vuex'

  export default {
      name: 'List',
      data() {
          return {
              articles: []
          }
      },
      computed: {
          ...mapState([
              'auth',
              'user',
          ])
      },
      beforeRouteEnter(to, from, next) {
          next(vm => {
              vm.articles = vm.$store.getters.getArticlesByUid(null, to.params.user)
          })
      }
  }
</script>

<style scoped>

</style>
