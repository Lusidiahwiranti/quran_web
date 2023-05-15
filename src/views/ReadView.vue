<script>
import NavItem from "../components/Nav.vue";
import FooterItem from "../components/Footer.vue";
import axios from "axios";
import { ref } from "vue";

export default {
  data() {
    return {
      surah: ref([]),
      translate: ref([]),
      audio: ref([]),
      allAyat: ref([]),
    };
  },

  components: {
    FooterItem,
    NavItem,
  },

  mounted() {
    this.getSurah();
    this.getAudio();
    this.getAyat();
  },

  methods: {
    getSurah() {
      axios
        .get(
          `https://api.quran.com/api/v4/chapters/${this.$route.params.id}?language=id`
        )
        .then((response) => {
          this.surah = response.data.chapter;
          this.translate = this.surah.translated_name;
        })
        .catch((error) => {
          console.log(error);
        });
    },
    getAudio() {
      axios
        .get(
          `https://api.quran.com/api/v4/chapter_recitations/7?chapter=${this.$route.params.id}`
        )
        .then((response) => {
          this.audio = response.data.audio_files[0];
        })
        .catch((error) => {
          console.log(error);
        });
    },
    getAyat() {
      axios
        .get(
          `https://api.quran.com/api/v4/quran/verses/uthmani_tajweed?chapter_number=${this.$route.params.id}`
        )
        .then((response) => {
          this.allAyat = response.data.verses;
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
};
</script>

<template>
  <NavItem />
  <main>
    <div class="container">
      <div class="row text-center mt-5">
        <div>
          <img src="../assets/al-quran.png" width="250" alt="logo" />
        </div>
        <div class="mt-5">
          <ul class="nav justify-content-center mb-5 nav-pills">
            <li class="nav-item">
              <router-link
                class="a nav-link"
                :class="{ active: $route.name === 'surah' }"
                :to="{ name: 'surah', params: { id: $route.params.id } }"
                >Translation</router-link
              >
            </li>
            <li class="nav-item">
              <router-link
                class="a nav-link"
                :class="{ active: $route.name === 'read' }"
                :to="{ name: 'read', params: { id: $route.params.id } }"
                >Reading</router-link
              >
            </li>
          </ul>
          <div class="d-flex justify-content-around">
            <div class="d-flex flex-column">
              <h2>{{ surah.name_complex }}</h2>
              <p>{{ translate.name }}</p>
            </div>
            <div class="d-flex flex-column">
              <h2>{{ surah.name_arabic }}</h2>
              <router-link
                class="a"
                :to="{ name: 'history', params: { id: $route.params.id } }"
              >
                <h5><i class="bi bi-info-circle"></i> Surah Info</h5>
              </router-link>
            </div>
          </div>
          <div class="my-1 text-center">
            <audio :src="audio.audio_url" controls></audio>
          </div>
        </div>
        <div class="mt-5">
          <div v-for="ayat in allAyat" :key="ayat.id">
            <div class="my-5" v-html="ayat.text_uthmani_tajweed"></div>
          </div>
        </div>
      </div>
    </div>
  </main>
  <FooterItem />
</template>

<style scoped>
.a {
  text-decoration: none;
  color: black;
}

.active {
  background-color: black !important;
}
</style>
