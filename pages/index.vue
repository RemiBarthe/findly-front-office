<script setup lang="ts">
interface Post {
  id: string;
  title: string;
  state: "published" | "archived" | "draft";
  createdBy: User;
  updatedBy: User | null;
  createdAt: Date;
  updatedAt: Date;
}

interface User {
  id: string;
  email: string;
  surname: string;
  createdBy: string | null;
  updatedBy: string | null;
  createdAt: Date;
  updatedAt: Date;
}

const { data } = await useFetch<Post[]>(
  "https://technical-test.findly.co/api/posts?page=1"
);

const posts: Post[] = data.value;
</script>

<template>
  <v-container>
    <v-row dense>
      <v-col v-for="post in posts" :key="post.title">
        <v-card>
          <v-card-title v-text="post.title"></v-card-title>

          <v-card-text>
            <div>{{ post.state }}</div>

            <div>{{ post.createdAt }}</div>
          </v-card-text>

          <v-card-actions>
            <v-btn color="primary"> Lire la suite </v-btn>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>
