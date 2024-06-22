<template>
  <q-page>
    <h1>Album Photos</h1>
    <q-list>
      <q-item v-for="photo in photos" :key="photo.id" clickable @click="viewPhoto(photo.url)">
        <q-item-section>
          <img :src="photo.thumbnailUrl" style="max-width: 100px; max-height: 100px;" />
        </q-item-section>
        <q-item-section>
          <q-item-label>{{ photo.title }}</q-item-label>
        </q-item-section>
      </q-item>
    </q-list>
    <q-dialog v-model="isPhotoDialogOpen">
      <img :src="currentPhotoUrl" style="max-width: 100%;" />
    </q-dialog>
  </q-page>
</template>

<script>
import { ref, onMounted } from 'vue';
import axios from 'axios';

export default {
  name: 'AlbumPhotos',
  props: {
    id: {
      type: Number,
      required: true
    }
  },
  setup(props) {
    const photos = ref([]);
    const isPhotoDialogOpen = ref(false);
    const currentPhotoUrl = ref('');

    const fetchPhotos = async () => {
      try {
        const response = await axios.get(`https://jsonplaceholder.typicode.com/photos?albumId=${props.id}`);
        photos.value = response.data;
      } catch (error) {
        console.error('Error fetching photos:', error);
      }
    };

    onMounted(fetchPhotos);

    const viewPhoto = (url) => {
      currentPhotoUrl.value = url;
      isPhotoDialogOpen.value = true;
    };

    return {
      photos,
      isPhotoDialogOpen,
      currentPhotoUrl,
      viewPhoto
    };
  }
};
</script>

<style scoped>
/* CSS khusus jika diperlukan */
</style>
