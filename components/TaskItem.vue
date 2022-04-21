<template>
  <v-list-item v-if="task" inactive>
    <v-list-item-action>
      <v-btn icon :color="iconColor" @click="changeStatus">
        <v-icon v-text="icon" />
      </v-btn>
    </v-list-item-action>
    <v-list-item-content>
      <v-list-item-title v-text="task.title" :class="[icon !== 'mdi-check' ? 'text-decoration-none' : 'text-decoration-line-through']" />
      <v-list-item-subtitle v-text="task.description" :class="[icon !== 'mdi-check' ? 'text-decoration-none' : 'text-decoration-line-through']" />
    </v-list-item-content>
    <v-list-item-action>
      <v-btn icon color="error" @click="removeTask">
        <v-icon>mdi-trash-can-outline</v-icon>
      </v-btn>
    </v-list-item-action>
  </v-list-item>
</template>

<script>
export default {
  name: 'TaskItem',

  props: {
    task: {
      type: Object,
      default: null
    }
  },

  methods: {
    removeTask () {
      this.$store.dispatch('task/remove', this.task.id)
    },
    changeStatus () {
      this.$store.dispatch('task/done', {id: this.task.id, done: !this.task.done})
    }
  },

  computed: {
    icon () {
      return this.task.done ? 'mdi-check' : 'mdi-reload-alert'
    },
    iconColor () {
      return this.task.done ? 'success' : 'warning'
    },
  },

}
</script>
