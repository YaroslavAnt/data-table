<template>
  <div class="home">
    <v-data-table :headers="headers" :items="tableData" class="elevation-1">
      <template v-slot:top>
        <v-toolbar flat color="white">
          <v-toolbar-title>Users</v-toolbar-title>
          <v-divider class="mx-4" inset vertical></v-divider>
          <v-spacer></v-spacer>
          <v-btn color="primary" @click.native="$router.push(`/form`)">Create user</v-btn>
        </v-toolbar>
      </template>

      <template v-slot:item.action="{ item }">
        <v-btn icon color="orange">
          <v-icon @click="initUpdateUser(item)">mdi-pencil</v-icon>
        </v-btn>
        <v-btn icon color="red">
          <v-icon @click="deleteUser(item)">mdi-delete</v-icon>
        </v-btn>
      </template>
    </v-data-table>
  </div>
</template>

<script>
export default {
  name: "Home",

  data: () => ({
    headers: [
      { value: "name", text: "Name" },
      { value: "surname", text: "Surname" },
      { value: "phone", text: "Phone", sortable: false },
      { value: "email", text: "Email", sortable: false },
      { value: "action", text: "Actions", sortable: false }
    ],
    tableData: JSON.parse(localStorage.getItem("users"))
  }),
  methods: {
    initUpdateUser(user) {
      localStorage.setItem("user", JSON.stringify({ ...user, isEdited: true }));
      this.$router.push("/form");
    },
    deleteUser(deletedUser) {
      const isConfirmed = confirm(
        `User ${deletedUser.surname} will be removed`
      );
      if (isConfirmed) {
        const newData = [...this.tableData].filter(
          user => user.email !== deletedUser.email
        );
        this.tableData = newData;
        localStorage.setItem("users", JSON.stringify(newData));
      }
    }
  },
  mounted() {
    localStorage.removeItem("user");
  }
};
</script>
