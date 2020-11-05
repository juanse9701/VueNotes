<template>
  <div :id="index" class="task">
    <b-card :class="{'green': dark}" class="border-card">
      <b-card-text>
        {{ text }}
      </b-card-text>
      <b-button size="sm" @click="removeTask" class="remove-task">X</b-button>
    </b-card>
  </div>
</template>

<script>
export default {
  name: "Task",
  props: ["text", "dark", "index"],
  methods: {
      removeTask() {
          this.$emit('removeTask', this.index)
      }
  }
};
</script>

<style lang="scss" scope>
.task {
  .border-card {
    border-top: solid 6px;

    &.green {
      border-color: #41b883;
    }

    &:not(.green) {
      border-color: #34495e;
    }

    .remove-task {
      color: #34495e;
      border-color: #34495e;
      background-color: white;
      border-radius: 50%;
      font-size: 0.7rem;
    }
  }
}
</style>