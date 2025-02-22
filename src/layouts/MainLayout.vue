<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar
        class="q-py-md bg-white flex justify-between"
        style="width: 100%"
      >
        <div class="row items-center">
          <q-img src="../assets/govpelogo.png" class="img-logo q-mr-md" />

          <div class="row flex items-center" v-if="userLogado">
            <p class="hello q-mr-md q-mb-none">Olá, Anderson</p>
            <p class="hello cursor-pointer no-margin" @click="logOut">Sair</p>
          </div>
        </div>

        <header class="navbar">
          <nav>
            <ul>
              <li>
                <a
                  @click="changeRoute('/')"
                  :class="{ 'active-border': model == '/' }"
                  >Pagina Inicial</a
                >
              </li>
              <li>
                <a
                  @click="changeRoute('/selecoes')"
                  :class="{ 'active-border': model == '/selecoes' }"
                  >Seleções</a
                >
              </li>
              <li>
                <a
                  @click="changeRoute('/registro')"
                  :class="{ 'active-border': model == '/registro' }"
                  >Cadastrar</a
                >
              </li>
              <li>
                <a
                  @click="changeRoute('/login')"
                  :class="{ 'active-border': model == '/login' }"
                  >Login</a
                >
              </li>
            </ul>
          </nav>
        </header>
      </q-toolbar>
    </q-header>
    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script setup lang="ts">
import { onMounted, ref, watch } from "vue";
import { useRoute, useRouter } from "vue-router";

const router = useRouter();
const route = useRoute();

const model = ref(route.path);

const userLogado = ref("");

function changeRoute(route: string) {
  model.value = route;
  router.push(model.value);
}

function logOut() {
  localStorage.removeItem("userLogado");
  userLogado.value = "";
  router.push("/login");
}

watch(route, () => {
  model.value = route.path;

  if (localStorage.getItem("userLogado")) {
    userLogado.value = JSON.parse(localStorage.getItem("userLogado") || "");
  }
});

onMounted(() => {
  if (localStorage.getItem("userLogado")) {
    userLogado.value = JSON.parse(localStorage.getItem("userLogado") || "");
  }
});
</script>

<style lang="scss">
a {
  cursor: pointer;
}
.img-logo {
  width: 300px;
  height: 65px;
}

.navbar {
  background: white;
  top: 0;
  left: 0;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.navbar ul li {
  display: inline-block;
  margin-right: 1.25rem;
}

.navbar nav ul li a {
  color: black;
  text-decoration: none;
  font-size: 1rem;
}

.active-border {
  border-bottom: 0.125rem solid #ffcc00;
}

.hello {
  color: black;
  font-size: 1rem;
}
</style>
