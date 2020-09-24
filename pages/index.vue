<template>
  <ul>
    <li v-for="content in contents" :key="content.id">
      <nuxt-link :to="`/${content.id}`">
        {{ content.title }}
      </nuxt-link>
    </li>
  </ul>
</template>

<script>
import axios from "axios";

export default {
  async asyncData() {
    const { data } = await axios.get(
      "https://jw0924.microcms.io/api/v1/blog",
      {
        headers: { "X-API-KEY": "a2679751-05f0-4365-8459-3c1da53ada00" },
      }
    );
    return data;
  },
};
</script>
