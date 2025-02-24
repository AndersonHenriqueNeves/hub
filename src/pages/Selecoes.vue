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
                class="q-mr-sm"
                label="Resultado preliminares"
                @click="downloadPdf(props.row.documentacao.resultado)"
              />
              <q-btn
                v-if="userLogged"
                color="black"
                label="Inscrever-se"
                @click="openUpload(props.row.selecao)"
              />
            </div>
          </q-td>
        </template>
      </q-table>
    </div>
  </q-page>
</template>

<script setup lang="ts">
import { onMounted, ref } from "vue";
import edital from "../assets/2. Edital.pdf";
import decreto from "../assets/1.Decreto Autorizativo.pdf";
import resultado from "../assets/9.Resultado Preliminar - 2ª Convocação.pdf";
import { useQuasar } from "quasar";
import DialogUpload from "src/components/DialogUpload.vue";
import { useRouter } from "vue-router";

const router = useRouter();

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

const $q = useQuasar();

const userLogged = ref(false);

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

function openUpload(selecao: string) {
  $q.dialog({
    component: DialogUpload,
  })
    .onOk(() => {
      console.log("onOk");
      const sel = localStorage.getItem("userSelecoes");
      let newSel = [];
      if (sel) {
        newSel = JSON.parse(sel);

        newSel.push({
          id: generateRandomNumber(1, 8),
          process: selecao,
          insc: generateRandomNumber(1, 8),
          cpf: userLogged.value.cpf,
          name: userLogged.value.nome,
        });
      } else {
        newSel.push({
          id: generateRandomNumber(1, 8),
          process: selecao,
          insc: generateRandomNumber(1, 8),
          cpf: userLogged.value.cpf,
          name: userLogged.value.nome,
        });
      }

      localStorage.setItem("userSelecoes", JSON.stringify(newSel));

      router.push("/inscricoes");
    })
    .onCancel(() => {
      // console.log('Cancel')
    })
    .onDismiss(() => {
      // console.log('I am triggered on both OK and Cancel')
    });
}

function generateRandomNumber(min: number, max: number) {
  return Math.floor(Math.random() * (max - min + 1)) + min;
}

onMounted(() => {
  const user = localStorage.getItem("userLogado");
  if (user) {
    userLogged.value = JSON.parse(user);
  }
});
</script>

<style lang="scss">
.bg-hub {
  background-color: #005f98;
}
</style>
