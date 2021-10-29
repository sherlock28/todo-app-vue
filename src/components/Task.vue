<template>
    <div>
        <h1 class="display-4 text-center">Listado de tareas</h1>
    </div>
    <div class="row">
        <div class="col-lg-8 offset-lg-2">
            <div class="card mt-2">
                <div class="card-body">
                    <div class="input-group">
                        <input v-model="task" type="text" class="form-control form-control-lg" placeholder="Agregar tarea"/>
                        <div class="input-group-append">
                            <button class="btn btn-success btn-lg" @click="addTask">Agregar</button>
                        </div>
                    </div>
                    <p v-if="isError && task === ''" class="text-danger">El campo no puede ser vacío.</p>
                    <hr/>
                    <h5 v-if="listTasks.length === 0">No hay tareas para realizar</h5>
                    <ul class="list-group">
                        <li v-for="(task, index) of listTasks" :key="index" class="list-group-item d-flex justify-content-between">
                            <span class="cursor" :class="{'text-success': task.state}" @click="changeState(task, index)">
                                <i :class="[task.state ? 'fas fa-check-circle' : 'far fa-circle']"></i>
                            </span>
                            {{task.name}}
                            <span class="text-danger cursor" @click="removeTask(index)"><i class="far fa-trash-alt"></i></span>
                        </li>
                    </ul>

                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name:"Task",
        data() {
            return {
                task: "",
                listTasks: [],
                isError: false
            }
        },
        methods: {
            addTask() {
                this.task !== "" ? this.createTask() : this.showError();
            },
            createTask() {
                const task = {
                    name: this.task,
                    state: false
                }
                this.listTasks.push(task);
                this.task = "";
                this.isError = false;
            },
            showError() {
                this.isError = true;
            },
            removeTask(index) {
                this.listTasks.splice(index, 1);
            },
            changeState(task, index) {
                this.listTasks[index].state = !task.state;
            }
        }
    }
</script>

<style scoped>
.cursor {
    cursor: pointer;
}
</style>