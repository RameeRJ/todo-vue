<template>
  <div class="container">
   <h2 class="text-center mt-5">my  vue todo app</h2>
   <div class="d-flex">
    <input v-model="task" @keydown.enter="submitTask" type="text" placeholder="Enter Task" class="form-control">
    <button @click="submitTask" class="btn btn-warning rounded-0" type="submit">Submit</button>
   </div>
   <table class="table table-bordered mt-5">
  <thead>
    <tr>
      <th scope="col">Task</th>
      <th scope="col">Status</th>
      <th scope="col" class="text-center">Edit</th>
      <th scope="col" class="=text-center">Delete</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(task,index) in tasks" :key="index">
      <td>{{task.name}}</td>
      <td style="width: 120px"><span @click="changeStatus(index)" class="pointer">{{task.status}}</span></td>
      <td>
        <div class="text-center" @click="editTask(index)">
          <span class="fa fa-pen"></span>
        </div>
      </td>
      <td>
        <div class="text-center" @click="deleteTask(index)">
          <span class="fa fa-trash"></span>
        </div>
      </td>
    </tr>
  </tbody>
</table>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },

  data() {
    return {
      task:'',
      editedTask: null,
      availableStatus: ['To-do', 'In-progress', 'Completed'],
      tasks: [
      ] 
    }
  },

  methods:{
    submitTask(){
     if(this.task.length === 0) return;


    if(this.editedTask === null){
     this.tasks.push({
      name: this.task,
      status: 'To-do'
     })
    }else{
      this.tasks[this.editedTask].name = this.task;
      this.editedTask = null;
    }
     this.task = '';
    },

    deleteTask(index){
      this.tasks.splice(index, 1);
    },

    editTask(index){
      this.task = this.tasks[index].name;
      this.editedTask = index;
    },

    changeStatus(index){
     let newIndex = this.availableStatus.indexOf(this.tasks[index].status);
    if(++newIndex > 2) newIndex = 0;

    this.tasks[index].status = this.availableStatus[newIndex];
    }
  }
};
</script>

<style scoped>
.pointer {
  cursor: pointer;
}
</style>
