<template>
  <div id="app">
    <h1>Things Todo</h1>
    <div id="todoList">
      <div id="noTasks" v-if="!todoList.length">You don't have any tasks yet.</div>
      <div id="noTasks" v-if="error">Task already exists.</div>
      <ul>
        <li
          v-for="task in todoList"
          :key="task.task"
          :class="{ done: task.done }"
        >
          <div
            :class="{ checkBox: true, done: task.done }"
            @click="toggleTask(task)"
          ></div>
          <span>{{ task.task }}</span>
          <i @click="deleteTask(task)" class="material-icons">delete</i>
        </li>
      </ul>
      <div id="newTask">
        <input
          @keyup.enter="addTask"
          v-model="newTask"
          type="text"
          placeholder="New task"
        />
        <button @click="addTask" :disabled="!newTask"><span>+</span></button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      todoList: [],
      newTask: "",
      error: false,
    };
  },
  methods: {
    addTask() {
      const exists = this.todoList.some((task) => task.task === this.newTask);

      if (exists) {
        this.error = true;

        setTimeout(() => (this.error = false), 3000);
      } else {
        this.todoList.push({
          task: this.newTask,
          done: false,
        });

        this.newTask = "";
      }
    },
    toggleTask(task) {
      task.done = !task.done;
    },
    deleteTask(task) {
      this.todoList = this.todoList.filter(t => t.task !== task.task);
    }
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

  ul {
    list-style: none;
    padding: 25px;
    li {
      display: flex;
      align-items: center;
      line-height: 1;
      user-select: none;
      &:not(:last-child) {
        padding-bottom: 15px;
      }
      .checkBox {
        width: 20px;
        height: 20px;
        border: 2px solid #ddd4ce;
        border-radius: 50%;
        margin-right: 15px;
        position: relative;
        display: flex;
        opacity: 0.7;
        transition: all 0.2s ease-in-out;
        &:hover {
          cursor: pointer;
          opacity: 1;
        }
        &:before {
          transition: all 0.2s ease-in-out;
          content: "\e876";
          font-family: "Material Icons";
          margin: auto;
          font-size: 0.8em;
          color: #31ecb8;
          opacity: 0;
          transform: scale(0.5);
        }
        &.done {
          border-color: #31ecb8;
          opacity: 1;
          &:before {
            opacity: 1;
            transform: scale(1);
          }
        }
      }
      i {
        margin-left: auto;
        padding-left: 15px;
        opacity: 0;
        color: #ff3c41;
        transition: all 0.2s ease-in-out;
        font-size: 1.2em;
      }
      &:hover {
        cursor: text;
        i {
          opacity: 1;
          cursor: pointer;
        }
      }
      span {
        position: relative;
        transition: all 0.2s ease-in-out;
        &:before {
          content: "";
          height: 1px;
          background: #c3bbb6;
          width: 0%;
          top: 50%;
          position: absolute;
          left: 0;
        }
      }
      &.done span {
        color: #c3bbb6;
      }
      &.done span:before {
        width: 100%;
      }
    }
  }
  #noTasks,
  #newTask {
    background: rgba(0, 0, 0, 0.05);
    padding: 15px;
    display: flex;
  }
  #newTask {
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
}

::placeholder {
  color: rgba(0, 0, 0, 0.3);
}
</style>
