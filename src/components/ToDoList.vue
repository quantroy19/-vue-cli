<template>
  <section>
    <li :class="{ active: checkDone }">
      <form v-if="isEdit" @submit.prevent="updateTodo">
        <input class="input-edit" type="text" :id="data.id" v-model="data.name" />
        <button class="btn btn-update">Update</button>
      </form>
      <span v-else>
        <input
          type="checkbox"
          v-model="checkDone"
          :value="checkDone"
          @click="$emit('checkDoneTodo', id)"
        />
        <p>{{ name }}</p>
        <button @click="editTodo" class="btn btn-edit">Edit</button>
        <button @click="$emit('delete', id)" class="btn btn-delete">Remove</button>
      </span>
    </li>
  </section>
</template>

<script>
export default {
  props: {
    id: {
      type: String,
      required: true
    },
    name: {
      type: String,
      required: true
    },
    checked: {
      type: Boolean,
      required: false,
      default: false
    }
  },
  data() {
    return {
      checkDone: this.checked,
      isEdit: false,
      data: {
        id: this.id,
        name: this.name
      }
    };
  },
  methods: {
    checkDoneTodo() {
      this.checkDone = !this.checkDone;
    },
    editTodo() {
      this.isEdit = true;
    },
    updateTodo() {
      this.$emit("update", this.data);
      this.isEdit = false;
    }
  }
};
</script>
<style scoped>
.input-edit {
  width: 50%;
  display: inline;
}
</style>