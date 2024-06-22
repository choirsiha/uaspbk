<template>
  <q-page>
    <h1>Albums</h1>
    <q-list>
      <q-item v-for="album in albums" :key="album.id" clickable @click="goToAlbum(album.id)">
        <q-item-section>{{ album.title }}</q-item-section>
      </q-item>
    </q-list>
  </q-page>
</template>

<script>
import { ref, onMounted } from 'vue';
import axios from 'axios';
import { useRouter } from 'vue-router';

export default {
  name: 'Albums',
  setup() {
    const albums = ref([]);
    const router = useRouter();

    const fetchAlbums = async () => {
      try {
        const response = await axios.get('https://jsonplaceholder.typicode.com/albums');
        albums.value = response.data;
      } catch (error) {
        console.error('Error fetching albums:', error);
      }
    };

    const goToAlbum = (id) => {
      router.push({ name: 'AlbumPhotos', params: { id } });
    };

    onMounted(fetchAlbums);

    return {
      albums,
      goToAlbum,
    };
  },
};
</script>

<style scoped>
/* CSS khusus jika diperlukan */
</style>
