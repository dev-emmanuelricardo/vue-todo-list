<template>
  <div class="new-task">
    <div class="elements">
    <input v-model="name" @keydown.enter="add" type="text" 
    placeholder="Digite sua tarefa" class="form-element" />
    <button @click="add" class="form-element" title="Clique para adicionar tarefa">&#10010;</button>
    <button @click="delAll" class="limpar" title="Apagar todas as tarefas">&#10006;</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      name: ""
    };
  },
  methods: {
    add() {
      this.$emit("taskAdded", { name: this.name });
      this.clear();
    },
    clear() {
      this.name = "";
    },
    delAll() {
      this.$emit("deleteAll");
    }
  }
};
</script>

<style>
.new-task {
  margin: 35px;
  width: 80%;
}

.form-element {
  outline: none;
  font-size: 2rem;
  border: 1px solid rgb(168, 168, 168);
  padding: 5px 10px 8px;
  color: #FFF;
}

input.form-element{
  width: 80%;
  background: #FFF2;
  border-top-left-radius: 8px;
  border-bottom-left-radius: 8px;
  font-size: 19px;
  align-self: center;
  padding: 10px;
  
}

button.form-element{
  border-left: none;
  background: rgba(0,0,0,0.1);
  border-top-right-radius: 8px;
  border-bottom-right-radius: 8px;
  cursor: pointer;
  font-size: 19px;
}

.elements {
  display: flex;
  justify-content: center;
}

button.limpar {
  border: none;
  background: none;
  cursor: pointer;
  margin-left: 25px;
  font-size: 25px;
  color: #fff;
  outline: none;
  font-size: 19px;
}

</style>
