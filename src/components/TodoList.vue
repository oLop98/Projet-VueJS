<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <div>
      Nombre de tâches finies : {{ completedTasksCount }} / {{ totalTasksCount }}
    </div>
    <div class="progress-bar">
      <div class="progress" :style="{ width: getProgressWidth() + '%' }">{{ getProgressPercentage() }}</div>
    </div>
    <div id="app">
      <div class="formulaire">
        <input type="text" v-model="nouvelleTache" placeholder="Ajouter une tâche" />
        <button @click="ajouterTache">Ajouter</button>
      </div>

      <div v-for="(tache, index) in taches" :key="index" class="task">
        <todo-task :task="tache" @supprimer="supprimerTache(index)" @task-updated="updateTaskStatus" />
        <button class="supprimer-btn" @click="supprimerTache(index)">Supprimer</button>
      </div>
    </div>
  </div>
</template>

<script>
import TodoTask from '@/components/TodoTask.vue';
import axios from 'axios';

export default {
  name: 'TodoList',
  props: {
    msg: String
  },
  components: {
    TodoTask
  },
  data() {
    return {
      nouvelleTache: '',
      taches: []
    };
  },
  computed: {
    totalTasksCount() {
      return this.taches.length;
    },
    completedTasksCount() {
      return this.taches.filter(task => task.fait).length;
    }
  },
  created() {
    this.fetchTasks();
  },
  methods: {
    async fetchTasks() {
      try {
        const response = await axios.get('https://jsonplaceholder.typicode.com/todos');
        this.taches = response.data.map(task => ({
          id: task.id,
          texte: task.title,
          fait: task.completed
        }));
      } catch (error) {
        console.error('Erreur :', error);
      }
    },
    ajouterTache(){
      if (this.nouvelleTache.trim()) {
        this.taches.push({
          id: this.taches.length + 1,
          texte: this.nouvelleTache,
          fait: false
        });
        this.nouvelleTache = '';
      }
    },
    supprimerTache(index){
      this.taches.splice(index, 1);
    },
    updateTaskStatus(taskId, isCompleted) {
      const taskIndex = this.taches.findIndex(task => task.id === taskId);
      if (taskIndex !== -1) {
        this.taches[taskIndex].fait = isCompleted;
      }
    },
    getProgressWidth() {
      const totalTasks = this.taches.length;
      const completedTasks = this.taches.filter(task => task.fait).length;
      return totalTasks === 0 ? 0 : (completedTasks / totalTasks) * 100;
    },
    getProgressPercentage() {
      const width = this.getProgressWidth();
      return width.toFixed(0) + '%';
    }
  }
}
</script>

<style scoped>

.hello {
  font-family: Arial, sans-serif;
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

.formulaire {
  margin-bottom: 20px;
  display: flex; 
}

.formulaire input[type="text"] {
  padding: 10px;
  width: calc(100% - 90px);
  border-radius: 5px 0 0 5px;
  border: 1px solid #ccc;
}

.formulaire button {
  padding: 10px 20px;
  border: none;
  background-color: #333;
  color: #fff;
  border-radius: 0 5px 5px 0;
  cursor: pointer;
}

.task {
  margin-bottom: 10px;
  background-color: #f2f2f2;
  padding: 10px;
  border-radius: 5px;
  display: flex;
  align-items: center;
}

.task .supprimer-btn {
  padding: 5px 10px;
  background-color: #333;
  color: #fff;
  border: none;
  border-radius: 3px;
  cursor: pointer;
  margin-right: 10px; 
  margin-left: auto; /* Pour aligner le bouton "Supprimer" à gauche */
}

.task input[type="checkbox"] {
  margin-right: 10px;
}

.task label {
  flex: 1;
}

.task s {
  text-decoration: line-through;
  color: #aaa;
}

.progress-bar {
  height: 20px;
  background-color: #f2f2f2;
  margin-bottom: 20px;
}

.progress {
  height: 100%;
  background-color: #333;
  display: flex;
  justify-content: center;
  align-items: center;
  color: #fff;
}
</style>
