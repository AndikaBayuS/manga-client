<template>
  <div class="container">
    <div class="grid 2xl:grid-cols-5 lg:grid-cols-4 md:grid-cols-3 sm:grid-cols-3 grid-cols-2 gap-4">
        <div v-for="(manga, index) in mangas.manga_list" :key="index">
          <router-link :to="{ name: 'manga.detail', params: { endpoint: manga.endpoint }}">
              <div class="rounded overflow-hidden shadow-md w-42 md:w-52 h-auto bg-gray-700">
                <img class="w-full h-52" :src="manga.thumb_potrait" alt="Thumbnail">
                <div class="px-4 pt-4">
                    <div class="font-bold text-xs mb-2 truncate overflow-ellipsis text-white">{{manga.title}}</div>
                </div>
                <div class="px-4 pb-2">
                    <span class="inline-block bg-gray-200 rounded-full px-2 py-1 text-xs font-semibold text-gray-700 mr-2 mb-2">{{manga.chapter}}</span>
                    <span class="inline-block bg-red-500 rounded-full px-2 py-1 text-xs font-semibold text-white mb-2">UP!</span>
                    <br>
                    <span class="inline-block bg-gray-200 rounded-full px-2 py-1 text-xs font-semibold text-gray-700 mr-2 mb-2">{{manga.type}}</span>
                </div>
              </div>
          </router-link>
        </div>
    </div>
    <PaginationRelease />
  </div>
</template>
<script>
import axios from "axios";
import { ref } from "vue";
import { useRoute } from "vue-router";

export default {
  name: "LatestManga",
  async setup() {
    let mangas = ref([]);
    const route = useRoute();

    await axios
    .get(`http://127.0.0.1:3000/api/manga/page/${route.params.page}`)
    .then((result) => {
        mangas.value = result.data;
    })
    .catch((err) => {
        console.log(err.response);
    });

    return {
      mangas,
    };
  },
};
</script>
