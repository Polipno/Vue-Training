<template>
  <body>
    <h1>Welcome to {{ shopName.toUpperCase() }} !</h1>

    <div v-show="time > 60">
      Bravo vous êtes rester plus de 60 seconde dans la cuisine.
    </div>
    <div v-show="count > 20">Bravo vous avez créer plus de 20 cookie.</div>
    <p>Timer: {{ timer }} seconde</p>
    <p>Cookie: {{ count }}</p>
    <button v-on:click="increment">cook</button>
    <button @:click="decrement">sell</button>
    <button @:click="sortCookies">organise</button>
    <h2>Menu</h2>
    <form action="" @submit="addCookie">
      <input type="text" placeholder="Nouveau Cookie" v-model="cookieName" />
      <button>Ajouter</button>
    </form>
    <ul>
      <li v-for="(cookie, index) in cookies" :key="index">
        {{ cookie }}
        <button @click="deleteCookie(cookie)">delete</button>
      </li>
    </ul>
  </body>
</template>

<script setup>
import { ref } from "vue";
const shopName = "Cookie Shop";
const count = ref(0);
const cookieName = ref("");
const timer = ref(0);
const cookies = ref(["Cookie", "Cookie rose", "Cookie en or"]);

setInterval(() => {
  timer.value++;
}, 1000);
const increment = () => {
  count.value++;
};
const decrement = () => {
  count.value--;
};
const deleteCookie = (cookie) => {
  cookies.value = cookies.value.filter((c) => c != cookie);
};
const sortCookies = () => {
  cookies.value.sort((a, b) => (a > b ? 1 : -1));
};
const addCookie = (event) => {
  event.preventDefault();
  cookies.value.push(cookieName.value);
  cookieName.value = "";
};
</script>

<style>
h1 {
  color: aquamarine;
}

body {
  background: #292929;
  color: aliceblue;
}
</style>
