<template>
    <v-app id="inspire">
        <v-navigation-drawer v-model="drawer" app>
            <v-list dense>
                <v-list-item link>
                    <v-list-item-action>
                        <v-icon>mdi-home</v-icon>
                    </v-list-item-action>
                    <v-list-item-content>
                        <v-list-item-title>Home</v-list-item-title>
                    </v-list-item-content>
                </v-list-item>
                <v-list-item link>
                    <v-list-item-action>
                        <v-icon>mdi-contact-mail</v-icon>
                    </v-list-item-action>
                    <v-list-item-content>
                        <v-list-item-title>Contact</v-list-item-title>
                    </v-list-item-content>
                </v-list-item>
            </v-list>
        </v-navigation-drawer>
        <v-app-bar app color="indigo" dark>
            <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
            <v-toolbar-title>Application</v-toolbar-title>
        </v-app-bar>
        <v-content>
            <p class="display-2 text-center">ToDo(not) List</p>
            <task-form @add:task="addTask" />
            <task-table :tasklist="tasklist" @delete:task="deleteTask" @edit:task="editTask" />
            <v-container class="fill-height" fluid>
                <v-row align="center" justify="center">
                    <v-col class="text-center">
                        <v-tooltip left>
                            <template v-slot:activator="{ on }">
                                <v-btn :href="source" icon large target="_blank" v-on="on">
                                    <v-icon large>mdi-code-tags</v-icon>
                                </v-btn>
                            </template>
                            <span>Source</span>
                        </v-tooltip>
                        <v-tooltip right>
                            <template v-slot:activator="{ on }">
                                <v-btn icon large href="https://codepen.io/johnjleider/pen/zgxeLQ" target="_blank" v-on="on">
                                    <v-icon large>mdi-codepen</v-icon>
                                </v-btn>
                            </template>
                            <span>Codepen</span>
                        </v-tooltip>
                    </v-col>
                </v-row>
            </v-container>
        </v-content>
        <v-footer color="indigo" app>
            <span class="white--text">&copy; 2019</span>
        </v-footer>
    </v-app>
</template>
<script>
import TaskTable from '@/components/TaskTable.vue'
import TaskForm from '@/components/TaskForm.vue'
export default {
    name: 'app',
    components: {
        TaskTable,
        TaskForm,
    },
    data() {
        return {
            tasklist: [{
                    id: 1,
                    name: 'sample task 1',
                    date: 'sample date 1',
                },
                {
                    id: 2,
                    name: 'sample task 2',
                    date: 'sample date 2',
                },
                {
                    id: 3,
                    name: 'sample task 3',
                    date: 'sample date 3',
                },
            ],
        }
    },
    methods: {
        addTask(task) {
            const lastId =
                this.tasklist.length > 0 ?
                this.tasklist[this.tasklist.length - 1].id :
                0;
            const id = lastId + 1;
            const newTask = { ...task, id };
            this.tasklist = [...this.tasklist, newTask];
        },
        deleteTask(id) {
            this.tasklist = this.tasklist.filter(
                task => task.id !== id
            )
        },
        editTask(id, updateTask) {
            this.tasklist = this.tasklist.map(task => task.id === id ? updateTask : task)
        }
    },
    mounted() {
      const hello = require("test-package-chocnut");
      hello.printMsg();
      // your code as normal js
   },
}
</script>