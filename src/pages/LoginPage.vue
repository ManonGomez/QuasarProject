<template>
  <div class="q-pa-md row justify-center fit">
    <q-form @submit="onSubmit" @reset="onReset" class="q-gutter-md login">
      <div class="row justify-center">
        <h1 class="text-h3 text-weight-thin blue-grey-12 q-mb-xs">
          SE CONNECTER
        </h1>
        <p class="text-h6 text-weight-thin blue-grey-12 q-mt-xs">
          Bienvenue chez Newtone
        </p>
      </div>
      <div class="q-pr-lg q-pl-lg">
        <q-input
          color="red-14"
          outlined
          outlined-color="red"
          v-model="text"
          label="Login"
          lazy-rules
          :rules="[(val) => (val && val.length > 0) || 'Field is required']"
        >
          <div class="text-grey icon-input">
            <q-icon name="font_download" />
          </div>
        </q-input>
        <q-input
          class="q-mt-xs"
          color="red-14"
          outlined
          outlined-color="red"
          v-model="text"
          label="Mot de passe"
          lazy-rules
          :rules="[(val) => (val && val.length > 0) || 'Field is required']"
        >
          <div class="text-grey icon-input">
            <q-icon name="font_download" />
          </div>
        </q-input>

        <div class="row justify-center q-mt-xs">
          <q-btn
            class="full-width"
            unelevated
            label="Se connecter"
            no-caps
            type="submit"
            color="light-blue-10"
          />
          <q-btn
            class="q-mt-xs text-weight-regular full-width"
            flat
            no-caps
            color="blue-grey-12"
            label="Mot de passe oublié ?"
          />
        </div>
      </div>
    </q-form>
  </div>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "LoginPage",
});
</script>
