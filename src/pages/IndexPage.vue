<template>
  <q-page class="q-pa-md">
    <h1>Bem-vindo ao novo hub de inscrição a seleções do Governo do Estado</h1>

    <div style="font-size: 1rem">
      <p>
        Esta página demonstra nossa capacidade de criar um ambiente simples e
        objetivo, oferecendo uma experiência intuitiva para candidatos
        interessados em participar de processos seletivos do Governo do Estado.
      </p>
    </div>
  </q-page>
</template>

<script setup lang="ts">
import { ref } from "vue";
import type { Todo, Meta } from "components/models";
import ExampleComponent from "components/ExampleComponent.vue";

const todos = ref<Todo[]>([
  {
    id: 1,
    content: "ct1",
  },
  {
    id: 2,
    content: "ct2",
  },
  {
    id: 3,
    content: "ct3",
  },
  {
    id: 4,
    content: "ct4",
  },
  {
    id: 5,
    content: "ct5",
  },
]);

const meta = ref<Meta>({
  totalCount: 1200,
});
</script>
