<template>
  <div id="app" style="width:960px">
    <img alt="Todo logo" src="./assets/logo.png" />
    <b-card class="text-center mt-4">
      <div>
        <b-form>
          <b-form-group
            id="input-group-1"
            label="Title:"
            label-for="input-1"
            description="The title should not be empty"
          >
            <b-form-input
              id="input-1"
              v-model="form.title"
              required
              placeholder="Enter some title"
            ></b-form-input>
          </b-form-group>
          <b-form-group
            id="input-group-2"
            label="Body:"
            label-for="input-2"
            description="The description should reveal the essence of the task."
          >
            <b-form-input
              id="input-2"
              v-model="form.body"
              required
              placeholder="Enter some description"
            ></b-form-input>
          </b-form-group>
          <b-form-group id="input-group-3">
            <b-form-checkbox id="checkboxes-3" v-model="form.completed">
              Completed
            </b-form-checkbox>
          </b-form-group>
          <b-form-group id="input-group-4">
            <b-button type="submit" variant="primary" @click.prevent="onAdd">
              Add
            </b-button>
            <b-button type="reset" variant="danger" @ckick.prevent="onReset">
              Reset
            </b-button>
          </b-form-group>
        </b-form>
      </div>
    </b-card>
    <b-card class="text-center mt-4">
      <div class="task-list">
        <ul v-if="tasks.length">
          <template v-for="(item, index) in tasks">
            <li
              :key="index"
              class="card"
              :class="item.completed ? 'task-comp' : 'task-not-comp'"
            >
              <div class="card-body">
                <h4 class="card-title">{{ item.title }}</h4>
                <p class="card-text">{{ item.body }}</p>
                <b-form-group id="input-group-4 mr-0">
                  <b-button
                    type="submit"
                    variant="primary"
                    @click="comletedTask(index)"
                  >
                    {{ item.completed ? "Not Completed" : "Completed" }}
                  </b-button>
                  <b-button
                    type="reset"
                    variant="danger"
                    @click="removeTask(index)"
                  >
                    Remove
                  </b-button>
                </b-form-group>
              </div>
            </li>
          </template>
        </ul>
        <div v-else>Tasks list is empty</div>
      </div>
    </b-card>
  </div>
</template>

<script>
export default {
  name: 'app',
  data: () => ({
    form: { title: '', body: '', completed: false },
    tasks: [
      { title: 'To buy', body: 'Buy bread for toast', completed: true },
      {
        title: 'Go to the cinema',
        body: 'Watch the new blockbuster with Stephen Seagal',
        completed: false
      },
      {
        title: 'To slepp',
        body: '',
        completed: true
      },
      {
        title: 'Call parents',
        body: 'Call parents and say that everything is in order',
        completed: false
      }
    ]
  }),
  methods: {
    onAdd (evn) {
      if (!this.form.title) return alert('Please input Title!')
      const { title, body, completed } = this.form
      this.tasks.push({ title, body, completed })
      this.onReset()
    },
    onReset (evn) {
      this.form.title = ''
      this.form.body = ''
      this.form.completed = false
    },
    removeTask (index) {
      this.tasks.splice(index, 1)
    },
    comletedTask (index) {
      this.tasks[index].completed = !this.tasks[index].completed
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: hsl(210, 29%, 24%);
  margin: 20px auto;
}

#input-group-4 {
  text-align: center;
}

.task-comp {
  color: #ccc;
}

.task-not-comp {
  color: #008;
}

.form-group {
  text-align: left;
}

.form-text {
  text-align: right;
}

.btn {
  margin: 0 0.25rem;
}

ul {
  padding: 0px;
}

li {
  margin: 10px 0;
  list-style: none inside;
}

.card {
  text-align: left;
}
</style>
