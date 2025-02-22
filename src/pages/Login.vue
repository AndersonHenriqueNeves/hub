<template>
  <div style="width: 100%" class="flex justify-center q-mt-md">
    <q-form @submit="submitForm" style="width: 50%">
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
        <q-btn label="Entrar" type="submit" color="primary" />
      </div>
    </q-form>
  </div>
</template>

<script setup>
import { ref } from "vue";
import { useRouter } from "vue-router";
const router = useRouter();
const form = ref({
  senha: "",
  email: "",
});

const showPassword = ref(false);

const submitForm = () => {
  if (localStorage.getItem("users")) {
    const users = JSON.parse(localStorage.getItem("users"));

    const findUser = users.find((e) => e.email == form.value.email);
    console.log(findUser);

    if (findUser) {
      if (findUser.senha == form.value.senha) {
        router.push("/selecoes");
      } else {
        alert("Email ou senha errado");
      }
    } else {
      alert("Email ou senha errado");
    }
  }

  //   router.push("/login");
};
</script>
