<template>
  <div>
    <AddItem
      :studentName="name"
      v-on:addBookToList="saveBook($event)"
      @callDailog="editDialog(item)"
      :dialogBox="dialog"
      :editItemProp="bookItem"
      :editIndexProp="bookIndex"
      :editBook="books"
    />
    <DeleteItem
      :deleteDialogBox="deleteDialog"
      :deleteBookIndex="bookIndex"
      :deleteBookItem="bookItem"
      :deleteBooks="books"
    />
    <v-data-table
      :headers="headers"
      :items="books"
      sort-by="authorName"
      class="elevation-1"
    >
      <template v-slot:[`item.actions`]="{ item }">
        <v-icon small class="mr-2" @click="editDialog(item)">
          mdi-pencil
        </v-icon>
        <v-icon small @click="deleteItem(item)"> mdi-delete </v-icon>
      </template>
    </v-data-table>
  </div>
</template>
<script>
import AddItem from "@/components/AddItem.vue";
import DeleteItem from "@/components/DeleteItem.vue";
export default {
  components: { AddItem, DeleteItem },
  data() {
    return {
      name: "Nainan",
      dialog: false,
      bookItem: null,
      deleteDialog: false,
      bookIndex: -1,

      headers: [
        {
          text: "Books",
          align: "start",
          sortable: false,
          value: "name",
        },
        { text: "Author Name", value: "authorName" },
        { text: "Published date", value: "publishedDate" },
        { text: "No. of pages", value: "noOfPages" },
        { text: "Actions", value: "actions", sortable: false },
      ],
      books: [
        {
          name: "The Winners",
          authorName: "Fredrik Backman",
          publishedDate: "September 27th 2022",
          noOfPages: 688,
        },
        {
          name: "Demon Copperhead",
          authorName: "Barbara Kingsolver",
          publishedDate: "October 18th 2022",
          noOfPages: 560,
        },
        {
          name: "How Not to Drown in a Glass of Water",
          authorName: "Angie Cruz",
          publishedDate: "September 13th 2022",
          noOfPages: 208,
        },
        {
          name: "Lucy by the Sea",
          authorName: "Elizabeth Strout",
          publishedDate: "September 20th 2022",
          noOfPages: 304,
        },
        {
          name: "To Paradise",
          authorName: "To Paradise",
          publishedDate: "January 11th 2022",
          noOfPages: 720,
        },
      ],
    };
  },
  watch: {
    addDialog(oldValue) {
      this.dialog = oldValue;
    },
  },
  methods: {
    saveBook(event) {
      console.log("In parent component", event);
      this.books.unshift(event);
      console.log(this.books);
    },
    editDialog(item) {
      this.dialog = true;
      this.bookItem = item;
      console.log(this.dialog);
      console.log("dialog called");
      this.bookIndex = this.books.indexOf(item);
      this.bookItem = Object.assign({}, item);
    },

    deleteItem(item) {
      this.deleteDialog = true;
      this.bookItem = item;
      console.log("delete item dialog: ", this.deleteDialog);
      this.bookIndex = this.books.indexOf(item);
      this.bookItem = Object.assign({}, item);
    },
  },
};
</script>

