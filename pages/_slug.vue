<template>
  <main class="main">
    <img :src="thumbnail && thumbnail.url">
    <picture v-if="thumbnail">
      <source
        media="(min-width: 768px)"
        type="image/webp"
        :srcset="`${thumbnail.url}?w=600&fm=webp, ${thumbnail.url}?w=1200&fm=webp 2x`"
      />
      <source
        media="(max-width: 768px)"
        type="image/webp"
        :srcset="`${thumbnail.url}?w=375&fm=webp, ${thumbnail.url}?w=750&fm=webp 2x`"
      />
      <img
        :src="`${thumbnail.url}?w=1200`"
        class="thumbnail"
        alt
      />
    </picture>
    <h1 class="title">{{ title }}</h1>
    <p class="publishedAt">{{ publishedAt }}</p>
    <p class="category">{{ category && category.name }}</p>
    <div class="post" v-html="body"></div>
  </main>
</template>

<script>
import axios from "axios";
export default {
  async asyncData({ params }) {
    const { data } = await axios.get(
      `https://jw0924.microcms.io/api/v1/blog/${params.slug}`,
      {
        headers: { "X-API-KEY": "a2679751-05f0-4365-8459-3c1da53ada00" },
      }
    );
    return data;
  },
};
</script>

<style lang="scss" scoped>
.main {
  width: 960px;
  margin: 0 auto;
}
.title {
  margin-bottom: 20px;
}
.publishedAt {
  margin-bottom: 40px;
}
.post {
  & > h1 {
    font-size: 30px;
    font-weight: bold;
    margin: 40px 0 20px;
    background-color: #eee;
    padding: 10px 20px;
    border-radius: 5px;
  }
  & > h2 {
    font-size: 24px;
    font-weight: bold;
    margin: 40px 0 16px;
    border-bottom: 1px solid #ddd;
  }
  & > p {
    line-height: 1.8;
    letter-spacing: 0.2px;
  }
  & > ol {
    list-style-type: decimal;
    list-style-position: inside;
  }
}
</style>
