<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar
        class="q-py-md bg-white flex justify-between"
        style="width: 100%"
      >
        <q-img src="../assets/govpelogo.png" class="img-logo" />

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
import { ref, watch } from "vue";
import { useRoute, useRouter } from "vue-router";

const router = useRouter();
const route = useRoute();

const model = ref(route.path);

function changeRoute(route: string) {
  model.value = route;
  router.push(model.value);
}

watch(route, () => {
  model.value = route.path;
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
</style>
