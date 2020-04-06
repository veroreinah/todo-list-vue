<template>
  <div id="newTask">
    <input
      @keyup.enter="addTask"
      v-model="newTask"
      type="text"
      placeholder="New task"
    />
    <button @click="addTask" :disabled="!newTask"><span>+</span></button>
  </div>
</template>

<script>
export default {
  name: "NewTask",
  data() {
    return {
      newTask: "",
    };
  },
  methods: {
    addTask() {
      this.$emit("addTask", this.newTask);
      
      this.newTask = "";
    },
  },
};
</script>

<style lang="scss">
#newTask {
  background: rgba(0, 0, 0, 0.05);
  padding: 15px;
  display: flex;
  input {
    flex: 1;
    margin-right: 10px;
    padding: 5px 10px;
    border: none;
    border-radius: 5px;
    outline: none;
    border-left: 2px solid #f65050;
    font-family: "Roboto", sans-serif;
  }
  button {
    outline: none;
    border: none;
    border-radius: 50%;
    font-size: 1.5em;
    color: white;
    background: #f65050;
    display: flex;
    width: 35px;
    height: 35px;
    transition: all 0.15s ease-in-out;
    span {
      margin: auto;
    }
    &:hover {
      cursor: pointer;
      background: #ff5c60;
    }
  }
}

::placeholder {
  color: rgba(0, 0, 0, 0.3);
}
</style>
