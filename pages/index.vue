<template>
  <section>
    <article
      v-for="(article, index) in articleList"
      :key="index"
      class="box media">
      <figure class="media-left">
        <p class="image is-64x64">
          <img :src="article.user.profile_image_url">
        </p>
      </figure>
      <div class="media-content">
        <div class="content">
          <p><strong><a :href="article.url">{{ article.title}}</a></strong><br>
            {{ article.user.id }}<br>
            <small>Like · {{ article.likes_count }}</small>
          </p>
        </div>
      </div>
    </article>
  </section>
</template>

<script>
// axios
import axios from 'axios';

// qiita api URL
const BASE_URL = 'https://qiita.com/api/v2/';

export default {
  async asyncData(context) {
    try {
      const response = await axios.get(BASE_URL + 'items', {
        params: {
          page: 1,
          per_page: 10,
          query: 'Nuxt.js',
        }
      });
      return {
        articleList: response.data,
      };
    } catch (error) {
      console.log(error);
    }
  }
}
</script>

<style>

.container {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}
</style>
