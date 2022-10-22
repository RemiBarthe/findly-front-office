<script setup lang="ts">
import { Post } from "@/types/post";
import { useRoute } from "vue-router";

const route = useRoute();
const id: string | string[] = route.params.id;

const { data: post, error } = await useFetch<Post>(
  () => `https://technical-test.findly.co/api/posts/${id}`,
  { key: `post:${id}` }
);
</script>

<template>
  <v-row v-if="error">{{ error }}</v-row>
  <v-row dense v-else>
    <v-btn variant="tonal" @click="$router.back()"> Button </v-btn>

    <h2>{{ post.title }}</h2>

    <p>{{ post.content }}</p>
  </v-row>
</template>
