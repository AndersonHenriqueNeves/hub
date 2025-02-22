<template>
  <div style="width: 100%" class="flex justify-center q-mt-md">
    <q-form @submit="submitForm" style="width: 50%">
      <q-input
        v-model="form.nome"
        label="Nome Completo"
        outlined
        dense
        :rules="[(val) => !!val || 'Nome é obrigatório']"
      />

      <q-input
        v-model="form.endereco"
        label="Endereço"
        outlined
        dense
        :rules="[(val) => !!val || 'Endereço é obrigatório']"
      />

      <q-input
        v-model="form.telefone"
        label="Telefone"
        mask="(##) #####-####"
        outlined
        dense
        :rules="[(val) => !!val || 'Telefone é obrigatório']"
      />

      <q-input
        v-model="form.cpf"
        label="CPF"
        mask="###.###.###-##"
        outlined
        dense
        :rules="[(val) => !!val || 'CPF é obrigatório']"
      />

      <q-input
        v-model="form.rg"
        label="RG"
        mask="##.###.###-#"
        outlined
        dense
        :rules="[(val) => !!val || 'RG é obrigatório']"
      />

      <q-input
        v-model="form.dataNascimento"
        label="Data de Nascimento"
        mask="##/##/####"
        outlined
        dense
        :rules="[(val) => !!val || 'Data de nascimento é obrigatória']"
      />

      <q-input
        v-model="form.email"
        label="Email"
        type="email"
        outlined
        dense
        :rules="[
          (val) => !!val || 'Email é obrigatório',
          (val) => /.+@.+\..+/.test(val) || 'Email inválido',
        ]"
      />

      <q-input
        v-model="form.senha"
        label="Senha"
        :type="showPassword ? 'text' : 'password'"
        outlined
        dense
        :rules="[(val) => !!val || 'Senha é obrigatória']"
      >
        <template v-slot:append>
          <q-icon
            :name="showPassword ? 'visibility' : 'visibility_off'"
            class="cursor-pointer"
            @click="showPassword = !showPassword"
          />
        </template>
      </q-input>

      <div class="q-mt-md">
        <q-btn label="Enviar" type="submit" color="primary" />
      </div>
    </q-form>
  </div>
</template>

<script setup>
import { ref } from "vue";
import { useRouter } from "vue-router";
const router = useRouter();
const form = ref({
  nome: "",
  endereco: "",
  telefone: "",
  cpf: "",
  rg: "",
  dataNascimento: "",
  senha: "",
  email: "",
});

const showPassword = ref(false);

const submitForm = () => {
  console.log(form.value);
  const users = localStorage.getItem("users")
    ? JSON.parse(localStorage.getItem("users"))
    : [];
  users.push(form.value);
  localStorage.setItem("users", JSON.stringify(users));
  router.push("/login");
};
</script>
