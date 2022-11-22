<template>
  <popup
    v-show="isModalVisible"
    :isModalVisible="isModalVisible"
    :isAddTask="isAddTask"
    :existing_description="description"
    :existing_deadline="deadline"
    :existing_priority="priority"
    :tasks="tasks"
    @submitTask="submitTask"
    @editTask="editTask"
    @close="closePopup"
  />

  <div class="container-fluid">
    <div class="card">
      <div
        class="card-header d-flex justify-content-between align-items-center"
      >
        <div class="col-sm-11">
          <h5 class="text-center">FRAMEWORKS</h5>
        </div>
        <div class="col-sm-1">
          <button
            @click="submitTaskPopup"
            type="button"
            class="btn btn-primary btn-sm"
          >
            <span class="fa-solid fa-circle-plus"></span> Add
          </button>
        </div>
      </div>
    </div>

    <div>
      <!--Task Table-->
      <table class="table table-bordered">
        <thead>
          <tr>
            <th scope="col">Title</th>
            <th scope="col">Description</th>
            <th scope="col">Deadline</th>
            <th scope="col">Priority</th>
            <th scope="col">Is Complete</th>
            <th scope="col">Action</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(task, index) in tasks" :key="index">
            <td>
              <span>{{ task.title }}</span>
            </td>
            <td>
              <span>{{ task.description }}</span>
            </td>
            <td>{{ task.deadline }}</td>
            <td>
              <span>{{ task.priority }}</span>
            </td>
            <td align="center">
              <label class="container">
                <input
                  type="checkbox"
                  v-model="tasks[index].isComplete"
                  @click="tasks[index].isComplete = !tasks[index].isComplete" />
                <span class="checkmark"></span
              ></label>
            </td>
            <td>
              <div>
                <button
                  v-if="!tasks[index].isComplete"
                  @click="editTaskPopup(index)"
                  class="btn btn-primary btn-block btn-sm w-75"
                >
                  <span class="fa-solid fa-pen-to-square"></span>
                  Update
                </button>
              </div>
              <div>
                <button
                  @click="deleteTask(index)"
                  class="btn btn-danger btn-block btn-sm w-75"
                >
                  <span class="fa-solid fa-circle-xmark"></span>
                  Delete
                </button>
              </div>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import popup from './popup';
export default {
  name: 'Todo',
  props: {
    msg: String,
  },
  components: {
    popup,
  },
  data() {
    return {
      isModalVisible: false,
      isAddTask: true,
      task: '',
      availablePriorities: ['Low', 'Med', 'High'],
      taskIndex: null,
      title: '',
      description: '',
      deadline: '',
      priority: 'low',
      tasks: [],
    };
  },
  methods: {
    submitTaskPopup() {
      this.isAddTask = true;
      this.showPopup();
    },

    editTaskPopup(index) {
      this.taskIndex = index;
      this.isAddTask = false;
      this.description = this.tasks[this.taskIndex].description;
      this.deadline = this.tasks[this.taskIndex].deadline;
      this.priority = this.tasks[this.taskIndex].priority;
      this.showPopup();
    },

    submitTask(title, description, deadline, priority) {
      this.tasks.push({
        title: title,
        description: description,
        deadline: deadline,
        priority: priority,
        isComplete: false,
      });
      this.$toast.success('The task was added successfully!');
    },

    editTask(description, deadline, priority) {
      this.tasks[this.taskIndex].description = description;
      this.tasks[this.taskIndex].deadline = deadline;
      this.tasks[this.taskIndex].priority = priority;
      this.$toast.success('The task was edited successfully!');
    },

    deleteTask(index) {
      this.tasks.splice(index, 1);
      this.$toast.success('The task was deleted successfully!');
    },

    showPopup() {
      this.isModalVisible = true;
    },
    closePopup() {
      this.isModalVisible = false;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
