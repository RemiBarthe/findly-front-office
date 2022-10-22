<script setup lang="ts">
import { Post } from "@/types/post";
import { useRoute } from "vue-router";
import { mdiArrowULeftTop } from "@mdi/js";
import moment from "moment";

const route = useRoute();
const id: string | string[] = route.params.id;

const { data: post, error } = await useFetch<Post>(
  () => `https://technical-test.findly.co/api/posts/${id}`,
  { key: `post:${id}` }
);

function formatDate(date: Date) {
  return moment(date).locale("en").fromNow();
}
</script>

<template>
  <v-row v-if="error">{{ error }}</v-row>
  <v-row v-else>
    <v-col>
      <h2 class="mb-4">
        <v-btn
          @click="$router.back()"
          :icon="mdiArrowULeftTop"
          size="small"
          class="mr-2"
        />
        {{ post.title }}
      </h2>

      <h3 class="text-subtitle-1">
        <v-chip size="small" class="mr-2">{{ post.state }}</v-chip
        >{{ formatDate(post.createdAt) }}
      </h3>

      <p class="my-8">{{ post.content }}</p>

      <p v-if="post.createdBy" class="text-subtitle-2">
        By {{ post.createdBy.surname }} ({{ post.createdBy.email }})
      </p>
    </v-col>
  </v-row>
</template>
