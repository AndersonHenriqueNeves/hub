<template>
  <q-page>
    <div class="q-pa-md flex justify-center" style="width: 100%">
      <q-table
        title="Seleções abertas"
        :rows="rows"
        :columns="columns"
        row-key="name"
        :rows-per-page-options="[0]"
        hide-pagination
        flat
      >
        <template v-slot:body-cell-documentacao="props">
          <q-td :props="props">
            <div class="flex row justify-between">
              <q-btn
                color="deep-orange"
                text-color="white"
                label="Decreto autorizativo"
                class="q-mr-sm"
                @click="downloadPdf(props.row.documentacao.decreto)"
              />
              <q-btn
                color="primary"
                label="Edital"
                class="q-mr-sm"
                @click="downloadPdf(props.row.documentacao.edital)"
              />
              <q-btn
                color="secondary"
                label="Resultado preliminares"
                @click="downloadPdf(props.row.documentacao.resultado)"
              />
            </div>
          </q-td>
        </template>
      </q-table>
    </div>
  </q-page>
</template>

<script setup lang="ts">
import { ref } from "vue";
import edital from "../assets/2. Edital.pdf";
import decreto from "../assets/1.Decreto Autorizativo.pdf";
import resultado from "../assets/9.Resultado Preliminar - 2ª Convocação.pdf";

const columns = ref([
  {
    name: "selecao",
    required: true,
    label: "Seleção",
    align: "left",
    field: (row) => row.selecao,
    format: (val) => `${val}`,
    sortable: true,
  },
  {
    name: "descricao",
    required: true,
    label: "Descrição",
    align: "left",
    field: (row) => row.descricao,
    format: (val) => `${val}`,
    sortable: true,
  },
  {
    name: "aberto",
    required: true,
    label: "Aberto até",
    align: "left",
    field: (row) => row.aberto,
    format: (val) => `${val}`,
    sortable: true,
  },
  {
    name: "documentacao",
    required: true,
    label: "Documentação",
    align: "left",
    field: (row) => row.documentacao,
    format: (val) => `${val}`,
  },
]);

const rows = ref([
  {
    selecao: "Professor",
    descricao:
      "Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dumm",
    aberto: "29/02/1998",
    documentacao: {
      edital: "edital",
      decreto: "decreto",
      resultado: "resultado",
    },
  },
  {
    selecao: "Aluno",
    descricao:
      "Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dumm",
    aberto: "29/02/1998",
    documentacao: {
      edital: "edital",
      decreto: "decreto",
      resultado: "resultado",
    },
  },
]);

const downloadPdf = (file: string) => {
  const link = document.createElement("a");

  if (file == "edital") {
    link.href = edital;
  }

  if (file == "decreto") {
    link.href = decreto;
  }

  if (file == "resultado") {
    link.href = resultado;
  }

  link.download = `${file}.pdf`;
  link.click();
};
</script>

<style lang="scss">
.bg-hub {
  background-color: #005f98;
}
</style>
