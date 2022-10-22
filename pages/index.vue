<script setup lang="ts">
import moment from "moment";
import { Post } from "@/types/post";

const { data } = await useFetch<Post[]>(
  "https://technical-test.findly.co/api/posts?page=1"
);

const posts: Post[] = data.value;

function formatDate(date: Date) {
  return moment(date).locale("en").fromNow();
}
</script>

<template>
  <v-container>
    <v-row dense align="start">
      <v-col v-for="post in posts" :key="post.title">
        <v-card>
          <v-card-title v-text="post.title"> </v-card-title>

          <v-card-subtitle>
            <v-chip size="x-small">{{ post.state }}</v-chip>
            {{ formatDate(post.createdAt) }}
          </v-card-subtitle>

          <v-card-actions>
            <v-btn color="primary" @click="$router.push('/posts/' + post.id)">
              Read more
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>
