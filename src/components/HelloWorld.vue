<template>
  <v-container >
    <v-row class="text-center">
      <v-col class="mb-4">
        <div class="containerTable">

        <!-- Add new task input -->
        <h1 class="display-2 font-weight-bold mb-3">Todo list</h1>
        <div style="margin-top: 50px" class="d-flex">
          <input
            style="border: 1px solid "
            v-model="newTodo"
            type="text"
            placeholder=" Enter new task..."
            id="input"
            
            />
          <v-btn @click="addTodo()"
           elevation="8"
          >ADD </v-btn>

        </div>

        <div v-if="todosArray.length === 0">
          <H3 style="margin-top: 50px"
            >The list is empty, please add some tasks.</H3
          >
        </div>

        <!-- Setup bootstrap table -->
        <div v-else class="tableBox ">
          <table class="table table-bordered mt-10">
            <thead>
              <tr>
                <th scope="col">#</th>
                <th scope="col">Task</th>
                <th scope="col">Done</th>
                <th scope="col" class="">Delete</th>
                <th scope="col" class="text-center">Edit</th>
              </tr>
            </thead>
            <tbody>

              <!--List tasks -->
              <tr
                v-bind:key="todo.index"
                v-for="(todo, index) in todosArray"
                style="font-weight: bold"
              >
               <!--Number of tasks -->
                <th class="col-md-1">{{ index + 1 }}</th>

               <!--If the task is completed line-through and background green -->
                <td 
                  v-if="!todosArray[index].isEditing && todosArray[index].completed"
                  class="table-success"
                   :class="{ done: todo.completed }"
                >
                {{ todo.text }}
                </td>
              
                 <!--If the user is editing a task, use Update button and add input -->
                <td  v-else  > 
                  <input   v-if="todosArray[index].isEditing"
                    style="border: 2px solid; border-radius: 4px; "
                    v-bind:value="todosArray[index].text"
                    id="inputEdit"
                    type="text"
                    onkeypress="this.style.width = ((this.value.length + 1) * 8) + 'px';"
                  />
                  <div v-else> {{ todo.text }} </div>
                </td>

                <td class="col-md-1">
                  <input
                    type="checkbox"
                    id="checkbox"
                    v-model="todo.completed"
                  />
                </td>

                <!--Delete a task -->
                <td class="col-md-1">
                  <div class="text-center">
                    <v-btn
                      color="#FF0000"
                      elevation="10"
                      x-small
                      @click="deleteTodo(index)"
                    >
                      Delete
                      <v-icon>mdi-delete </v-icon>
                    </v-btn>
                  </div>
                </td>

                 <!-- if user is editing a task, Edit a task (Update btn) -->
                <td  class="col-md-1" v-if="todosArray[index].isEditing">
                  <v-btn
                    color="#AFEEEE"
                    elevation="10"
                    x-small
                    v-if="todosArray[index].isEditing"
                    @click="editTodo(index)"
                  >
                    Update

                    <i class="material-icons">create</i>
                  </v-btn>
                </td>


                <!--Edit a task button (user not updating) -->
                <td  class="col-md-1" v-else>
                  <v-btn
                    color="#C0C0C0"
                    elevation="10"
                    x-small
                    @click="changeEditButton(index)"
                  >
                    Edit

                    <i class="material-icons">create</i>
                  </v-btn>
                </td>
              </tr>
            </tbody>
          </table>
        </div>
        </div>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: "HelloWorld",

  data() {
    return {
      newTodo: "",
      existingTodo: "",
      isEditing: false,
      todosArray: [
        { text: "Create a todo list", completed: false, isEditing: false },
        { text: "Learn Vue.Js", completed: false, isEditing: false },
      ],
    };
  },
  methods: {
    addTodo() {
      if (this.newTodo !== "")
        this.todosArray.push({
          text: this.newTodo,
          completed: false,
          isEditing: false,
        });
      this.newTodo = "";
    },
    editTodo(index) {
      this.todosArray[index].isEditing = false;
      this.todosArray[index].text = this.existingTodo;
      this.todosArray[index].text = document.getElementById("inputEdit").value;
    },
    deleteTodo(index) {
      this.todosArray.splice(index, 1);
    },
    changeEditButton(index) {
      this.todosArray[index].isEditing = true;
    },
   
  },
};
</script>

<style >
.done {
  text-decoration: line-through;
}
#input{
  width: 100%;
}
</style>