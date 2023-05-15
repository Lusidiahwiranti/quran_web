<script setup>
import NavItem from "../components/Nav.vue";
import FooterItem from "../components/Footer.vue";
</script>

<template>
  <NavItem />
  <main>
    <div class="container">
      <div class="row mt-5">
        <div class="text-center">
          <img src="../assets/al-quran.png" width="250" alt="logo" />
        </div>
        <div class="mt-5">
          <h1>About Us</h1>
          <p>
            Al-Quran was founded in 2022. The website aims to make it easy for anyone to read, study, and learn the Quran.
          </p>
        </div>
        <div class="my-5">
          <h1>Credits</h1>
          <p>
            First of All,by the grace of Allah,I have become able to create this website to make Al-Qur'an available to all the people in online. Actually,I used An API which is developed by some great developers and i also take the idea of FrontEnd of this website from Quran.com . Thanks to Quran.com's developers to give us a great API and cool Quran website. And,the final thing ,i have to say ,otherwise Credit section will incomplete, that my brother is a great person who helps encouraging me always time to learn.I used my brother's laptop to build up this website.
            I salute my brother as he helps me every single time giving me All.
          </p>
        </div>
      </div>
    </div>
  </main>
  <FooterItem />
</template>
