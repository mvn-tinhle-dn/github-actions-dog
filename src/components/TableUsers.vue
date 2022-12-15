<script>

export default {
  name: "TableUsers",
  props: { dataUser: Array, deleteUser: Function, handleEdit: Function, setIsEdit: Function },
  methods: {
    handleDeleteUser(id) {
      this.deleteUser(id);
    },
    handleEditUser(value) {
      this.setIsEdit()
      this.handleEdit(value);
    }
  }

}

</script>

<style scoped>
table,
th,
td {
  border: 1px solid #ccc;
  border-collapse: collapse;
  padding: 0 30px;
  min-width: 200px;
}

th {
  text-align: left;
}

thead {
  background-color: darkgray;
}

td:not(th) {
  padding: 8px 30px;
}

table {
  width: 445px;
}

.td-action {
  display: flex;
  gap: 10px
}

button {
  min-width: 89px;
  cursor: pointer;
}
</style>

<template>
  <table>
    <thead>
      <th>
        Name
      </th>
      <th>
        Action
      </th>
    </thead>
    <tbody>
      <tr v-for="user in dataUser" v-bind:key="user.id">
        <td>{{ user.userName }}</td>
        <td class="td-action">
          <button @click="handleDeleteUser(user.id)">Delete</button>
          <button @click="handleEditUser(user)">Edit</button>
        </td>
      </tr>
    </tbody>
  </table>
</template>