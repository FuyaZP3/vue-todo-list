<template>
  <v-dialog max-width="290" v-model="openAddTask">
    <template #activator="{ on }">
      <v-btn icon v-on="on">
        <v-icon>mdi-plus</v-icon>
      </v-btn>
    </template>
    <v-card shaped elevation="24">
      <v-card-title class="secondary">
        Add Task
      </v-card-title>
      <v-card-text>
        <v-form ref="form" lazy-validation>
          <v-text-field
            v-model="form.title"
            :rules="rules.title"
            label="Title"
            requried
          />
          <v-text-field
            v-model="form.description"
            :rules="rules.description"
            label="Description"
            requried
          />
        </v-form>
      </v-card-text>
      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn color="teal" text @click="saveTask">Save</v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  name: 'AddTaskItem',

  data () {
    return {
      openAddTask: false,
      form: {
        title: null,
        description: null
      },
      rules: {
        title: [
          v => !!v || 'Title is requried',
          v => (!!v && v.length >= 2) || 'Title must be bigger than 2 charachers'
        ],
        description: [
          v => !!v || 'Description is requried',
          v => (!!v && v.length <= 50) || 'Description must be less than 50 charachers'
        ]
      }
    }
  },

  methods: {
    saveTask() {
      if(this.$refs.form.validate()) {
        this.$store.dispatch('task/add', this.form)
        this.$refs.form.reset()
        this.openAddTask = false
      }
    }
  }
}
</script>
