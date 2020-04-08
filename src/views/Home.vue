<template>
  <div class="home">
    <v-data-table
      :headers="headers"
      :items="getProductsForTable"
      :server-items-length='productsData.total'
      :currentPage.sync="currentPage"
      :pageCount='productsData.last_page'
      hide-default-footer
      class="elevation-1"
    >
      <template v-slot:top>
        <v-toolbar
          flat
          color="white"
        >
          <v-toolbar-title>Категория: {{getCategoryFromParams}}</v-toolbar-title>
          <v-divider
            class="mx-4"
            inset
            vertical
          ></v-divider>
          <v-spacer></v-spacer>
          <v-dialog
            v-model="dialog"
            max-width="500px"
          >
            <template v-slot:activator="{ on }">
              <v-btn
                v-on="on"
                color="primary"
                dark
                class="mb-2"
                @click="addItem()"
              >Добавить товар</v-btn>
            </template>
            
          </v-dialog>
        </v-toolbar>
      </template>

      

      

      <template v-slot:item.action="{ item }">
        <v-icon
          small
          class="mr-2"
          @click="editItem(item)"
        >mdi-pencil</v-icon>
        <v-icon
          small
          @click="deleteItem(item)"
        >mdi-delete</v-icon>
      </template>
    </v-data-table>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";

export default {
  name: "Home",
  components: {
    HelloWorld
  }
};
</script>
