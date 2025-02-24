<template>
  <div class="cont flex justify-center q-mt-md">
    <q-table
      title="Inscrições"
      :rows="rows"
      :columns="columns"
      row-key="name"
      :rows-per-page-options="[0]"
      hide-pagination
      flat
    >
    </q-table>
  </div>
</template>

<script setup>
import { onMounted, ref } from "vue";
import { useRouter } from "vue-router";

const columns = ref([
  {
    name: "id",
    required: true,
    label: "#",
    align: "left",
    field: (row) => row.id,
    format: (val) => `${val}`,
    sortable: true,
  },
  {
    name: "process",
    required: true,
    label: "Processo Seletivo",
    align: "left",
    field: (row) => row.process,
    format: (val) => `${val}`,
    sortable: true,
  },
  {
    name: "insc",
    required: true,
    label: "Número de Inscrição",
    align: "left",
    field: (row) => row.insc,
    format: (val) => `${val}`,
    sortable: true,
  },
  {
    name: "cpf",
    required: true,
    label: "CPF",
    align: "left",
    field: (row) => row.cpf,
    format: (val) => `${val}`,
  },
  {
    name: "name",
    required: true,
    label: "Nome Completo",
    align: "left",
    field: (row) => row.name,
    format: (val) => `${val}`,
  },
]);

const rows = ref([]);

const router = useRouter();
onMounted(() => {
  const sel = localStorage.getItem("userSelecoes");
  if (sel) {
    rows.value = JSON.parse(sel);
  }
});
</script>

<style lang="scss">
.cont {
  width: 100%;
}
</style>
