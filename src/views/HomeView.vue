<script setup lang="ts">
import { ref } from 'vue';
import type { Ref } from 'vue';
const name: Ref<string> = ref('');
const lastname: Ref<string> = ref('');
const genero: Ref<string> = ref('');
const age: Ref<number> = ref(0);

const errors: any = ref([
]);

const validations = () => {
  limpiar();
  // NAME
  if (name.value.length > 18) {
    errors.value.push("mucho texto");
  }

  if (name.value.length < 5) {
    errors.value.push("poco texto");
  }
  // LASTNAME
  if (lastname.value.length == name.value.length) {
    errors.value.push("No utilices tu nombre");
  }
  // AGE
  if (age.value > 60) {
    errors.value.push("mucho edad");
  }

  if (age.value < 0) {
    errors.value.push("poca edad");
  }

}
const limpiar = () => {
  errors.value = []
}
</script>

<template>
  <main>
    <form>
      <div>
        <h1 class="mayu">Formulario </h1>
      </div>
      <!-- ERRORES -->
      <div class="error">
        <h3>Mensajes :</h3>
        <span v-for="(error, index) in errors" :key="index">
          {{ error }} <br>
        </span>
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
      <!-- BTN -->
      <button>Enviar</button>
    </form>
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
  box-shadow: 5px 2px 2px 1px #41b883;
}

form div input {
  height: 45px;
  border-radius: 15px;
  border: 1px solid #41b883;
}

select {
  height: 45px;
  background: #f9f9f9;
  border-radius: 15px;
}

button {
  cursor: pointer;
  font-weight: bold;
  background: #41b883;
  height: 45px;
  color: white;
  border-radius: 15px;
}

button:hover {
  background: transparent;
  border: 1px solid #41b883;
  color: #41b883;
}

.mayu {
  text-transform: uppercase;
  color: #0c0c0c;
  font-size: 20PX;
}

.error {
  margin-top: 10px;
  text-align: center;
  color: rgb(0, 0, 0);
  border: 1px solid red;
  border-radius: 15px;
}
</style>
