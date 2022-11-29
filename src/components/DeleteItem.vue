<template>
  <v-row justify="center">
    <v-dialog v-model="deleteDialog" persistent max-width="290">
      <v-card>
        <v-card-title class="text-h5"> Confirmation </v-card-title>
        <v-card-text>Do you really want to delete this item? </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="green darken-1" text @click="deleteDialogfn()">
            Not Confirm
          </v-btn>
          <v-btn color="green darken-1" text @click="confirmDelete()">
            Confirm
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-row>
</template>
<script>
export default {
  name: "DeleteItem",
  data: () => ({
    deleteDialog: false,
    deleteItem: {
      name: "",
      authorName: "",
      publishedDate: "",
      noOfPages: 0,
    },
    defaultItem: {
      name: "",
      authorName: "",
      publishedDate: "",
      noOfPages: 0,
    },
    deleteIndex: -1,
    books: [],
  }),
  props: {
    deleteDialogBox: Boolean,
    deleteBookIndex: Number,
    deleteBookItem: Object,
    deleteBooks: Array,
  },
  watch: {
    deleteDialogBox(newValue) {
      this.deleteDialog = newValue;
      this.deleteItem = this.deleteBookItem;
      this.deleteIndex = this.deleteBookIndex;
      this.books = this.deleteBooks;
    },
  },
  methods: {
    deleteDialogfn() {
      this.deleteDialog = false;
      this.$emit("closeDeleteDialog", this.deleteDialog)
    },
    closeDelete() {
      this.dialogDelete = false;
      this.deleteItem = Object.assign({}, this.defaultItem);
      this.deleteIndex = -1;
    },
    confirmDelete() {
      this.$emit("confirmDeleteDialog", this.deleteDialog)
      this.deleteDialog = false;
      this.books.splice(this.deleteIndex, 1);
      this.closeDelete();
    },
  },
};
</script>