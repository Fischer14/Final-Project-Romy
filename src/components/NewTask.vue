<template>
    <div class="add-task">
        <h1>Add a new Task ☑️</h1>
        
        <div v-if="showErrorMessage">
            <p class="error-text">{{ errorMessage }}</p>
        </div>
        
        <div>
            <div class="input-field">
                <input type="text" placeholder="Add a Task Title" v-model="name">
            </div>
            
            <div class="input-field">
                <textarea class="input-field-new-task" type="text" placeholder="Add a Task Description" v-model="description" style="height: 10rem;"></textarea>
            </div>
            
            <button @click="addTask" class="add-btn">Add</button>
        </div>
    </div>
</template>

<script setup>
import { ref, reactive } from "vue";
import { useTaskStore } from "../stores/task";   

const taskStore = useTaskStore();

// variables para los valors de los inputs
const name = ref('');
const description = ref('');

// constant to save a variable that holds an initial false boolean value for the errorMessage container that is conditionally displayed depending if the input field is empty
const showErrorMessage = ref(false);

// const constant to save a variable that holds the value of the error message
const errorMessage = ref(null);

// Arrow function para crear tareas.
const addTask = () => {
    if(name.value.length === 0 || description.value.length === 0){
        // Primero comprobamos que ningún campo del input esté vacío y lanzamos el error con un timeout para informar al user.

        showErrorMessage.value = true;
        errorMessage.value = 'The task title or description is empty';
        setTimeout(() => {
        showErrorMessage.value = false;
        }, 5000);

    } else {
        // Aquí mandamos los valores a la store para crear la nueva Task. Esta parte de la función tenéis que refactorizarla para que funcione con emit y el addTask del store se llame desde Home.vue.

        taskStore.addTask(name.value, description.value);
        name.value = '';
        description.value = '';
    }
};

</script>

<style scoped>

div .add-task {
  margin: 10px auto;
  margin-top: 20px;
  padding: 20px;
  width: 30%;
  background: #FFFFFF;
  border-radius: 7px;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  box-shadow: 0 0 3px 2px #090b6f85;
}

div .add-task h1 {
    text-transform: uppercase;
    color: #0f5257;
    font-size: 2vmax;
    font-weight: 700;
}
div .error-text {
    color: red;
}

div input {
    width: 20em;
    padding-left: 2px;
    margin-top: 5px;
    margin-bottom: 10px;
    font-size: 16px;
    border-radius: 5px;
}

div textarea {
    width: 30em;
    padding-left: 2px;
    margin-top: 5px;
    margin-bottom: 10px;
    font-size: 16px;
    border-radius: 5px;
}

.add-btn {
  padding: 15px;
  font-size: 12px;
  text-transform: uppercase;
  letter-spacing: 2.5px;
  font-weight: 700;
  color: #fff;
  background: #0f5257;
  border: none;
  border-radius: 30px;
}

</style>
  