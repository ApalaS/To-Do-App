<template>
  <div>
    <div class="container">
      <input
        v-model="taskGiven"
        class="input is-primary"
        type="text"
        placeholder="Enter work"
      />
      <input
        v-model="prioritySet"
        class="input is-primary"
        type="number"
        min="0"
        max="10"
        placeholder="Enter priority"
      />
      <button @click="addTask" class="button is-primary is-light">
        SUBMIT
      </button>
    </div>
    {{ editedTask }}
    <div class="taskTable">
      <table class="table">
        <thead>
          <tr>
            <th><abbr title="serial-number">S.No</abbr></th>
            <th>Task</th>
            <th>priority</th>
            <th>status</th>
            <th>EDIT</th>
            <th>DELETE</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(task, index) in tasks" :key="index">
            <td>{{ index + 1 }}</td>
            <td>{{ task.name }}</td>
            <td
              v-bind:style="[
                task.priority < 5
                  ? { background: 'green' }
                  : { background: 'red' },
              ]"
            >
              <div>
                {{ task.priority }}
              </div>
            </td>
            <td>
              <span class="is-clickable" @click="changeStatus(index)">
                {{ task.status }}
              </span>
            </td>
            <td class="is-clickable">
              <div class="resetTask " @click="resetMe(index)">
                <span class="fa fa-pen"></span>
              </div>
            </td>
            <td class="is-clickable">
              <div class="deleteTask" @click="deleteMe(index)">
                <span class="fa fa-trash"></span>
              </div>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      taskGiven: "",
      prioritySet: "",
      statusRn: "to-do",
      editedTask: null,
      statuses: ["to-do", "in-progress", "done"],
      tasks: [],
    };
  },
  methods: {
    addTask: function() {
      if (this.taskGiven == '' || this.prioritySet == '') {
        alert("please enter task & priority");
        return;
      }
      if (this.editedTask == null) {
        this.tasks.push({
          name: this.taskGiven,
          status: this.statusRn,
          priority: this.prioritySet,
        });
      } else {
        this.tasks[this.editedTask].name = this.taskGiven;
        this.tasks[this.editedTask].priority = this.prioritySet;
        this.editedTask = null;
      }
      this.taskGiven = '',
      this.prioritySet = ''
    },
    deleteMe: function(index) {
      this.tasks.splice(index, 1); //splice
    },
    resetMe: function(index) {
      this.taskGiven = this.tasks[index].name;
      this.prioritySet = this.tasks[index].priority;
      this.editedTask = index;
    },
    changeStatus: function(index) {
      let newIndex = this.statuses.indexOf(this.tasks[index].status)+1;
      if (newIndex > 2) {
        newIndex = 0;
      }
      this.tasks[index].status = this.statuses[newIndex];
    },
  },
};
</script>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
}
input {
  max-width: 80%;
  margin-bottom: 10px;
}
.taskTable {
  margin-top: 30px;
  display: flex;
  justify-content: center;
  max-width: 100%;
}
button {
  max-width: 40%;
  margin-bottom: 10px;
}
</style>
