<template>
  <div :class="{ task: true, done: task.done }">
    <div
      :class="{ checkBox: true, done: task.done }"
      @click="toggleTask"
    ></div>
    <span>{{ task.task }}</span>
    <i @click="deleteTask" class="material-icons">delete</i>
  </div>
</template>

<script>
export default {
  name: "ListItem",
  props: ["task"],
  methods: {
    toggleTask() {
      this.$emit("toggleTask");
    },
    deleteTask() {
      this.$emit("deleteTask");
    },
  },
};
</script>

<style lang="scss">
.task {
  display: flex;
  align-items: center;
  line-height: 1;
  user-select: none;
  padding-bottom: 15px;

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
    &:before {
      width: 100%;
    }
  }
}
</style>
