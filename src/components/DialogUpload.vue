<template>
  <q-dialog ref="dialogRef" @hide="onDialogHide">
    <q-card class="q-dialog-plugin">
      <div class="q-pa-md">
        <div>
          <q-file filled bottom-slots v-model="rg" label="RG" counter>
            <template v-slot:prepend>
              <q-icon name="cloud_upload" @click.stop.prevent />
            </template>
            <template v-slot:append>
              <q-icon
                name="close"
                @click.stop.prevent="rg = null"
                class="cursor-pointer"
              />
            </template>
          </q-file>
        </div>

        <div>
          <q-file filled bottom-slots v-model="cpf" label="CPF" counter>
            <template v-slot:prepend>
              <q-icon name="cloud_upload" @click.stop.prevent />
            </template>
            <template v-slot:append>
              <q-icon
                name="close"
                @click.stop.prevent="cpf = null"
                class="cursor-pointer"
              />
            </template>
          </q-file>
        </div>

        <div>
          <q-file
            filled
            bottom-slots
            v-model="locale"
            label="Comprovante de residência"
            counter
          >
            <template v-slot:prepend>
              <q-icon name="cloud_upload" @click.stop.prevent />
            </template>
            <template v-slot:append>
              <q-icon
                name="close"
                @click.stop.prevent="locale = null"
                class="cursor-pointer"
              />
            </template>
          </q-file>
        </div>

        <div>
          <q-file
            filled
            bottom-slots
            v-model="xp"
            label="Comprovação de experiência"
            counter
          >
            <template v-slot:prepend>
              <q-icon name="cloud_upload" @click.stop.prevent />
            </template>
            <template v-slot:append>
              <q-icon
                name="close"
                @click.stop.prevent="model = null"
                class="cursor-pointer"
              />
            </template>
          </q-file>
        </div>

        <q-card-actions>
          <q-btn color="primary" label="OK" @click="onOKClick" />
          <q-btn color="primary" label="Cancel" @click="onDialogCancel" />
        </q-card-actions>
      </div>
    </q-card>
  </q-dialog>
</template>

<script setup>
import { useDialogPluginComponent } from "quasar";
import { ref } from "vue";

defineEmits([...useDialogPluginComponent.emits]);

const { dialogRef, onDialogHide, onDialogOK, onDialogCancel } =
  useDialogPluginComponent();

const rg = ref(null);
const cpf = ref(null);
const locale = ref(null);
const xp = ref(null);
function onOKClick() {
  onDialogOK();
}
</script>
