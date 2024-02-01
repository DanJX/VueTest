<script setup lang="ts">
import { ref } from 'vue';
import type { Ref } from 'vue';
const name: Ref<string> = ref('');
const lastname: Ref<string> = ref('');
const genero: Ref<string> = ref('');
const age: Ref<number> = ref(0);

const errors = ref([{

}
]);

const validations = () => {

  // NAME
  if (name.value.length > 18) {
    errors.value.push({ name: "mucho texto" });
  }

  if (name.value.length < 5) {
    errors.value.push({ name: "poco texto" });
  }
  // LASTNAME
  if (lastname.value.length == name.value.length) {
    errors.value.push({ name: "NO PUEDES PONER TU NOMBRE EN EL APELLIDO" });
  }
  // AGE
  if (age.value > 60) {
    errors.value.push({ age: "mucho edad" });
  }

  if (age.value < 0) {
    errors.value.push({ age: "poca edad" });
  }
}
</script>

<template>
  <main>
    <form>
      <div>
        <h1 class="mayu">Formulario </h1>
      </div>
      <!-- NAME -->
      <div>
        <input @input="validations()" v-model="name" type="text" placeholder="Introduce tu nombre">
      </div>
      <!-- LASTNAME -->
      <div>
        <input @input="validations()" v-model="lastname" type="text" placeholder="Introduce tu apellido">
      </div>
      <!-- EDAD -->
      <div>
        <input @input="validations()" v-model="age" type="number" placeholder="Introduce tu edad">
      </div>
      <!-- GENERO -->
      <div>
        <select v-model="genero">
          <option value="" selected disabled>Selecciona una opcion</option>
          <option value="masc">Masculino</option>
          <option value="feme">Femenino</option>
          <option value="otro">Otro</option>
        </select>
        <input v-if="genero === 'otro'" type="text" placeholder="Especifica otro género">
      </div>
      <button @submit="validations()">Enviar</button>
    </form>
    <div class="error">
      <h3>Errors :</h3>
      <span v-for="(error, index) in errors" :key="index">
        {{ error }}
      </span>
    </div>
  </main>
</template>

<style scoped>
form {
  background: #f9f9f9;
  border-radius: 25px;
  text-align: center;
  padding: 10px 20px;
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.mayu {
  text-transform: uppercase;
  color: #0c0c0c;
}

.error {
  text-align: center;
  color: rgb(255, 255, 255);
  background: rgb(255, 0, 0);
}
</style>
