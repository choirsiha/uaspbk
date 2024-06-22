<template>
  <q-page>
    <h1>Posts</h1>
    <q-select v-model="selectedUser" :options="users" label="Select User" @update:model-value="fetchPosts" />
    <q-list>
      <q-item v-for="post in posts" :key="post.id">
        <q-item-section>{{ post.title }}</q-item-section>
        <q-item-section>{{ post.body }}</q-item-section>
      </q-item>
    </q-list>
  </q-page>
</template>

<script>
import { ref, onMounted } from 'vue';
import axios from 'axios';

export default {
  name: 'Posts',
  setup() {
    const selectedUser = ref(null);
    const users = ref([]);
    const posts = ref([]);

    const fetchUsers = async () => {
      const response = await axios.get('https://jsonplaceholder.typicode.com/users');
      users.value = response.data.map(user => ({ label: user.name, value: user.id }));
    };

    const fetchPosts = async (userId) => {
      const response = await axios.get(`https://jsonplaceholder.typicode.com/posts?userId=${userId}`);
      posts.value = response.data;
    };

    onMounted(fetchUsers);

    return {
      selectedUser,
      users,
      posts,
      fetchPosts,
    };
  },
};
</script>
