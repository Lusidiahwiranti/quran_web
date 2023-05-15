<script>
import NavItem from "../components/Nav.vue";
import FooterItem from "../components/Footer.vue";
import axios from "axios";
import { ref } from "vue";

export default {
  data() {
    return {
      allInfo: ref([]),
      surah: ref([]),
    };
  },

  components: {
    NavItem,
    FooterItem,
  },

  mounted() {
    this.getInfo();
    this.getSurah();
  },

  methods: {
    getInfo() {
      axios
        .get(
          `https://api.quran.com/api/v4/chapters/${this.$route.params.id}/info?language=id`
        )
        .then((response) => {
          this.allInfo = response.data.chapter_info;
        })
        .catch((error) => {
          console.log(error);
        });
    },
    getSurah() {
      axios
        .get(
          `https://api.quran.com/api/v4/chapters/${this.$route.params.id}?language=id`
        )
        .then((response) => {
          this.surah = response.data.chapter;
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
        <div class="mb-5">
          <img src="../assets/al-quran.png" width="250" alt="logo" />
        </div>
        <div class="a mb-3 text-white d-flex justify-content-around">
          <p class="mt-3">{{ surah.name_complex }}</p>
          <p class="mt-3">{{ surah.verses_count }} Ayat</p>
          <p class="mt-3">Diturunkan di {{ surah.revelation_place }}</p>
        </div>
        <div v-html="allInfo.text"></div>
      </div>
    </div>
  </main>
  <FooterItem />
</template>

<style scoped>
.a {
  background-color: black;
}
</style>
