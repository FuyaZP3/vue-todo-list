<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="6">
      <v-card max-width="475" class="mx-auto" elevation="24" shaped>
        <v-toolbar color="secondary">
          <v-app-bar-nav-icon>
            <v-icon>mdi-format-list-bulleted-square</v-icon>
          </v-app-bar-nav-icon>
          <v-toolbar-title>ToDo List</v-toolbar-title>
          <v-spacer />
          <AddTaskItem />
        </v-toolbar>
        <!-- List -->
        <v-list>
          <v-list-group no-action>
            <template #activator >
              <v-list-item-title class="grey--text customSub">
                <v-badge 
                  color="secondary"
                  :content="progressTasks.length == 0 ? '0' : progressTasks.length"
                >
                  In Progress Tasks
                </v-badge>
              </v-list-item-title>
            </template>
            <v-list-item-group>
              <TaskItem
                v-for="(task, i) in progressTasks"
                :key="i"
                :task="task"
              />
            </v-list-item-group>
          </v-list-group>

          <v-list-group no-action>
            <template #activator>
              <v-list-item-title class="grey--text customSub"> 
                <v-badge
                  color="secondary"
                  :content="doneTasks.length == 0 ? '0' : doneTasks.length"
                >
                  Done Tasks
                </v-badge>
              </v-list-item-title>
            </template>
            <v-list-item-group>
              <TaskItem 
                v-for="(task, i) in doneTasks" 
                :key="i" 
                :task="task" 
              />
            </v-list-item-group>
          </v-list-group>
        </v-list>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
import TaskItem from '../components/TaskItem.vue'
import AddTaskItem from '../components/AddTaskItem.vue'
import {mapGetters} from 'vuex'

export default {
  name: 'IndexPage',
  components: {
    TaskItem,
    AddTaskItem
  },

  computed: {
    ...mapGetters({
      doneTasks: 'task/doneTasks',
      progressTasks: 'task/progressTasks',
    }),
  },
}
</script>

<style lang="scss">
  .customSub {
    @include sub-text;
  }
</style>
