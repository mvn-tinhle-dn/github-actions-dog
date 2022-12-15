<script>
import TableUsers from './TableUsers.vue';

export default {
  name: "Todo",
  components: { TableUsers },
  created() {
    localStorage.setItem("arrayUser", JSON.stringify([{ id: 1, userName: "Mem 1" }]))
  },
  mounted() {
    this.dataUser = JSON.parse(localStorage.getItem("arrayUser"))
    console.log("Minh");
    console.log("phen");
    console.log("cong");
    console.log("cong");
  },

  data() {
    return {
      value: "",
      isEdit: false,
      dataUser: [],
      valueUpdate: { id: "", userName: "" },
    }
  },

  methods: {
    deleteUser(value) {
      const indexDel = this.dataUser.findIndex(user => user.id === value);
      this.dataUser.splice(indexDel, 1);
      localStorage.setItem("arrayUser", JSON.stringify(this.dataUser));
    },
    handleADD() {
      if (this.isEdit) {
        this.dataUser.forEach((userItem, idex) => {
          if (userItem.id === this.valueUpdate.id) {
            this.isEdit = false;
            this.dataUser[idex].userName = this.value;
            localStorage.setItem("arrayUser", JSON.stringify(this.dataUser));
            this.value = "";
          }
        })
      }
      else
        if (this.value.trim() !== "") {
          this.dataUser = [{ id: Math.floor(Math.random() * 10000), userName: this.value }, ...this.dataUser];
          localStorage.setItem("arrayUser", JSON.stringify(this.dataUser));
          this.value = "";
        }
    },
    handleEdit(valueUser) {
      this.value = valueUser.userName;
      this.valueUpdate = valueUser;
    },
    setIsEdit() {
      this.isEdit = true;
    }
  }

}


</script>

<style scoped>
.div-1 {
  height: 36px;
  display: flex;
  margin-bottom: 36px;
}

input {
  width: 400px;
  border-radius: 8px;
  border: 1px solid #ccc;
  outline: unset;
  padding: 0 10px;
  border-top-right-radius: unset;
  border-bottom-right-radius: unset;
}

button {
  border-top-right-radius: 8px;
  border-bottom-right-radius: 8px;
  padding: 0 10px;
  border: 1px solid #ccc;
  border-left: unset;
}

button:hover {
  background-color: #242424;
  border: 1px solid #242424;
  color: #fff;
  cursor: pointer;
}
</style>

<template>
  <div class="div-1">
    <input type="text" v-model="value">
    <button @click="handleADD">{{ isEdit ? "Edit User" : "Add User" }}</button>
  </div>
  <TableUsers :dataUser="dataUser" :deleteUser="deleteUser" :handleEdit="handleEdit" :setIsEdit="setIsEdit" />
</template>
