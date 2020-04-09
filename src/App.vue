<template>
  <div id="app">
    <h1>Things Todo</h1>
    <div id="todoList">
      <div id="noTasks" v-if="!todoList.length">You don't have any tasks yet.</div>
      <div id="noTasks" v-if="error">Task already exists.</div>

      <div class="list">
        <ListItem
          v-for="task in todoList"
          :key="task.task"
          :task="task"
          @deleteTask="deleteTask(task)"
          @toggleTask="toggleTask(task)" />
      </div>
      
      <NewTask @addTask="addTask" />
    </div>
  </div>
</template>

<script>
import NewTask from "@/components/NewTask";
import ListItem from "@/components/ListItem";

export default {
  name: "App",
  data() {
    return {
      todoList: [],
      error: false,
    };
  },
  methods: {
    addTask(newTask) {
      const exists = this.todoList.some((task) => task.task === newTask);

      if (exists) {
        this.error = true;

        setTimeout(() => (this.error = false), 3000);
      } else {
        this.todoList.push({
          task: newTask,
          done: false,
        });
      }
    },
    deleteTask(task) {
      this.todoList = this.todoList.filter(t => t.task !== task.task);
    },
    toggleTask(task) {
      task.done = !task.done;
    }
  },
  components: {
    NewTask,
    ListItem
  },
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css?family=Kristi|Roboto");
@import url("https://fonts.googleapis.com/icon?family=Material+Icons");

* {
  padding: 0;
  margin: 0;
}

html {
  width: 100%;
  height: 100%;
}

body {
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  font-family: "Roboto", sans-serif;
  font-size: 15px;
  background: linear-gradient(to bottom, #9cedff 0%, #3e82c3 100%);
}

h1 {
  font-family: "Kristi", cursive;
  color: white;
  margin-bottom: 20px;
  font-size: 4em;
  font-weight: normal;
}

#todoList {
  width: 300px;
  box-shadow: -2px 2px 2px -1px rgba(0, 0, 0, 0.15);
  border-radius: 8px;
  background: white;
  overflow: hidden;

  .list {
    padding: 25px;
  }

  #noTasks {
    background: rgba(0, 0, 0, 0.05);
    padding: 15px;
    display: flex;
  }
}
</style>
