<script setup lang="ts">
import { Post } from "@/types/post";
import { useRoute } from "vue-router";

const route = useRoute();
const id: string | string[] = route.params.id;

const { data } = await useFetch<Post>(
  "https://technical-test.findly.co/api/posts/" + id
);

const post: Post = data.value;
</script>

<template>
  <v-container>
    <v-row dense>
      <v-btn variant="tonal" @click="$router.back()"> Button </v-btn>

      <h2>{{ post.title }}</h2>

      <p>{{ post.content }}</p>
    </v-row>
  </v-container>
</template>
