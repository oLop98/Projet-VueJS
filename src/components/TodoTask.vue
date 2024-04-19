<template>
  <div class="task">
    <input type="checkbox" v-model="task.fait" />
    <label :for="'cbTask'+task.id">{{ task.texte }}</label>
  </div>
</template>

<script>
export default {
  name: 'TodoTask',
  props: {
    task: Object
  },
  methods: {
    supprimerTache() {
      this.$emit('supprimer', this.task.id);
    }
  }
};
</script>

<style scoped>
.task {
  margin-bottom: 10px;
}

.task input[type="checkbox"] {
  margin-right: 10px;
}
</style>