<template>
    <div>
       <ul>
            <li v-for="task in tasks" v-text="task"></li>

       </ul>
       <input type="text" v-model="newTask" @blur="addTask">
    </div>
</template>

<script>
    export default {
        data(){
            return {
                // tasks:[],
                project:this.dataProject,
                newTask:''
            };

        },
        created(){
            // axios.get('/tasks').then(response =>(this.tasks = response.data));
            window.Echo.channel('tasks').listen('TaskCreated',({task})=>{
                this.addTask($task)
            });
        },
        methods:{

            save(){
                axios.post(`api/projects/${this.project.id}/tasks`,{body:this.newTask})
                .then(response => response.data)
                .then(this.addTask);
            },
            addTask(){
               
                this.project.tasks.push(this.newTask);
                this.newTask = '';
            }
        }
    }
</script>
