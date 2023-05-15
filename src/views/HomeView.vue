<script>
import NavItem from "../components/Nav.vue";
import FooterItem from "../components/Footer.vue";
import axios from "axios";
import { ref } from "vue";

export default {
  data() {
    return {
      allSurah: ref([]),
      search: "",
    };
  },

  components: {
    NavItem,
    FooterItem,
  },

  mounted() {
    this.getAllSurah();
  },

  computed: {
    filterSurah: function () {
      return this.allSurah.filter((allSurah) => {
        return allSurah.name_simple.toLowerCase().split("-").join(" ").match(this.search);
      });
    },
  },

  methods: {
    getAllSurah() {
      axios
        .get("https://api.quran.com/api/v4/chapters?language=id")
        .then((response) => {
          this.allSurah = response.data.chapters;
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
          <input class="form-control form-control-lg mb-5 font-italic" type="text" v-model="search" placeholder="Hellow brother what do you want to read?" />
          <p>Mostly people search</p>
        </div>
        <div class="col">
          <router-link
            class="btn btn-dark"
            :to="{ name: 'surah', params: { id: 67 } }"
            >Al - Mulk</router-link
          >
        </div>
        <div class="col">
          <router-link
            class="btn btn-dark"
            :to="{ name: 'surah', params: { id: 36 } }"
            >Yaseen</router-link
          >
        </div>
        <div class="col">
          <router-link
            class="btn btn-dark"
            :to="{ name: 'surah', params: { id: 18 } }"
            >Al - Kahf</router-link
          >
        </div>
        <div class="col">
          <router-link
            class="btn btn-dark"
            :to="{ name: 'surah', params: { id: 56 } }"
            >Al - Waqi'ah</router-link
          >
        </div>
      </div>
      <div class="surahs-overview-section__surahs-container mt-5">
        <div class="row">
          <div v-for="(surah, index) in filterSurah" :key="index" class="col-md-4 my-3">
            <router-link
              class="a"
              :to="{ name: 'surah', params: { id: surah.id } }"
            >
              <div class="surah flex p-3" data-id="{{ surah.id }}" tabindex="0">
                <div class="flex">
                  <div class="surah__id-container bg-secondary">
                    <span class="surah__id-body text-white">{{
                      surah.id
                    }}</span>
                  </div>
                  <div class="surah__eg-name flow">
                    <p>{{ surah.name_complex }}</p>
                    <p>{{ surah.translated_name.name }}</p>
                  </div>
                </div>
                <div class="surah__ar-name flow">
                  <p>{{ surah.name_arabic }}</p>
                  <p>
                    <span>{{ surah.verses_count }}</span> Ayahs
                  </p>
                </div>
              </div>
            </router-link>
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
.btn {
  border-radius: 25px;
}

.surahs-overview-section__surahs-container {
  display: grid;
  gap: 1rem;
}

.surahs-overview-section__surahs-container .surah {
  gap: 0rem;
  -webkit-box-pack: justify;
  justify-content: space-between;
  border-radius: 4px;
  box-shadow: #00000026 1.95px 1.95px 2.6px;
  transition: 0.15s;
  cursor: pointer;
  --flow-space: 0.35rem;
}

.surahs-overview-section__surahs-container .surah:hover {
  gap: 0rem;
  -webkit-box-pack: justify;
  justify-content: space-between;
  border-radius: 4px;
  box-shadow: #00000026 1.95px 1.95px 2.6px;
  transition: 0.15s;
  cursor: pointer;
  --flow-space: 0.35rem;
  background-color: black;
  color: white;
}

.surahs-overview-section__surahs-container .surah .surah__id-container {
  display: grid;
  place-items: center;
  width: 2.375rem;
  height: 2.375rem;
  margin-right: 0.64rem;
  border-radius: 4px;
  transform: rotate(45deg);
  transition: 0.15s;
}

.surahs-overview-section__surahs-container
  .surah
  .surah__id-container
  .surah__id-body {
  transform: rotate(-45deg);
}

.surahs-overview-section__surahs-container .surah .surah__ar-name {
  text-align: center;
}

.surahs-overview-section__surahs-container .surah * {
  word-break: break-word;
}

.flex {
  display: flex;
  gap: 1rem;
}
</style>
