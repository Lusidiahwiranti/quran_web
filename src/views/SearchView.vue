<script>
import NavItem from "../components/Nav.vue";
import { ref } from "vue";
import axios from "axios";

export default {
    components: {NavItem},
  data() {
    return {
      cari: "",
      surah: ref([]),
      judul: ref([]),
      arti: ref([]),
      suara: "",
      name: [],
    };
  },

  watch: {
    cari() {
      this.getSurah();
      this.getJudul();
      this.getArti();
      this.getSuara();
    },
  },

  mounted() {
    this.getSurah();
    this.getJudul();
    this.getArti();
    this.getSuara();
  },

  methods: {
    getSurah() {
      axios
        .get(
          "https://api.quran.com/api/v4/quran/verses/uthmani?chapter_number=" +
            this.cari
        )
        .then((response) => {
          this.surah = response.data.verses;
        })
        .catch((error) => {
          console.log(error);
        });
    },
    getJudul() {
      axios
        .get(
          "https://api.quran.com/api/v4/chapters/" + this.cari + "?language=id"
        )
        .then((response) => {
          this.judul = response.data.chapter;
          this.name = this.judul?.translated_name;
        })
        .catch((error) => {
          console.log(error);
        });
    },
    getArti() {
      axios
        .get(
          "https://api.quran.com/api/v4/quran/translations/39?chapter_number=" +
            this.cari
        )
        .then((response) => {
          this.arti = response.data.translations;
        })
        .catch((error) => {
          console.log(error);
        });
    },

    getSuara() {
      axios
        .get("https://api.quran.com/api/v4/chapter_recitations/4/" + this.cari)
        .then((response) => {
          this.suara = response.data.audio_file;
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
};
</script>

<template>
    <nav-item/>
    <div class="row text-center mt-5">
        <div>
            <img src="../assets/al-quran.png" width="300" alt="logo" />
        </div>

    </div>
  <div class="text-center">
    <h1>Masukkan nomor surah!</h1>
    <input
      v-model="cari"
      class="form-control me-2"
      type="search"
      placeholder="Search"
      aria-label="Search"
    />
   <div v-if="cari">
     <div class="mt-5">
       <h1>{{ judul?.name_complex }}</h1>
       <br />
       <h1>{{ name?.name }}</h1>
       <br />
       <h2>Diturunkan di {{ judul?.revelation_place }}</h2>
     </div>
     <p v-if="suara" class="text-lg-center mt-3">
       <audio v-bind:src="suara?.audio_url" controls></audio>
     </p>
   </div>
  </div>
  <div v-if="cari" v-for="(ayat, index) in surah" :key="index" class="card">
    <div class="card-body">
      <h5 class="card-title text-lg-end">
        {{ ayat?.text_uthmani }}{{ ayat?.verse_key }}
      </h5>
<!--      <p class="card-title text-end" v-html="arti[index].text"></p>-->
      <p class="card-title text-end">{{arti[index]?.text}}</p>

    </div>
  </div>
</template>

<style scoped></style>
