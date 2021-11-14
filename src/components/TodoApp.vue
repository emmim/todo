<template>
<div class="container">
    <h2 class="text-center mt-5">MY LIST TO DO!!</h2>

    <!-- input text -->
    <div class="d-flex">
        <input v-model="task" type="text" placeholder="Enter list Name" class="form-control">
        <button @click="submitTask" class="btn btn-primary rounded-0">ADD</button>
    </div>
    <!-- Task Table -->
    <table class="table table-bordered mt-4">
        <thead>
            <tr>
                <th scope="col">Task</th>
                <th scope="col">Status</th>
                <th scope="col" class="text-center">#</th>
                <th scope="col" class="text-center">#</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="(task, index) in tasks" :key="index">
                <td>
                   <span :class="{'done': task.status === 'done'}">
                    {{task.name}}
                   </span>
                    
                </td>
                <td style="width:120px">
                    <span @click="changeStatus(index)" class="pointer" :class="{'text-danger': task.status === 'to-do',
                    'text-warning': task.status === 'in-process',
                    'text-success': task.status === 'done'}">
                    {{ uppercase(task.status) }}
                    </span>
                    </td>
                <td>
                    <div class="text-center pointer" @click="editTask(index)">
                        <span class="fa fa-pen">
                        </span>
                    </div>
                </td>
                <td>
                     <div class="text-center pointer" @click="deleteTask(index)">
                        <span class="fa fa-trash">
                        </span>
                    </div>
                </td>
            </tr>
        </tbody>
    </table>
</div>
</template>

<script>
export default {
    data(){
        return{
            task: '',
            updateTask: null,
            availablestatus: ['to-do', 'in-process', 'done'],
            tasks: [
                {
                    name: 'make money from betting',
                    status: 'to-do'
                },
                {
                    name: 'make from programming this week',
                    status: 'done'
                }
            ]
        }
    },
    methods: {
        submitTask () {
            if(this.task.length === 0) return;
        if(this.updateTask === null){
            this.tasks.push({
                name:this.task,
                status: 'to-do'
            })
        }else{
            this.tasks[this.updateTask].name = this.task
            this.updateTask = null
        }
            this.task = ''
        },
        deleteTask(index) {
            this.tasks.splice(index, 1)
        },
    editTask(index){
       this.task = this.tasks[index].name
       this.updateTask = index
    },
    changeStatus(index){
       let newIndex = this.availablestatus.indexOf(this.tasks[index].status)

       if(++newIndex > 2)  newIndex = 0
       this.tasks[index].status = this.availablestatus[newIndex]
    },
    uppercase(str){
        return str.charAt(0).toUpperCase() + str.slice(1)
    }


    },
}
</script>


<style scoped>
    .pointer{
        cursor: pointer;
    }
    .done{
        text-decoration:line-through;
    }
    .container{
         background: linear-gradient(to bottom, #33ccff 0%, #ff99cc 100%);
         min-height: 80vh;
    }
</style>
