<template>
  <v-row justify="center">
    <v-btn rounded small color="primary" dark @click="dialog = true">
      Add Item
    </v-btn>
    <v-dialog v-model="dialog" persistent max-width="600px">
      <v-card>
        <v-card-title>
          <span class="text-h5">{{ formTitle }}</span>
        </v-card-title>
        <v-card-text>
          <v-container>
            <v-row>
              <v-col cols="12" sm="6" md="4">
                <v-text-field
                  label="Book Name"
                  v-model="addItem.name"
                ></v-text-field>
              </v-col>
              <v-col cols="12" sm="6" md="4">
                <v-text-field
                  label="Author Name"
                  v-model="addItem.authorName"
                ></v-text-field>
              </v-col>
              <v-col cols="12" sm="6" md="4">
                <v-text-field
                  label="Published Date"
                  v-model="addItem.publishedDate"
                ></v-text-field>
              </v-col>
              <v-col cols="12">
                <v-text-field
                  label="No. of Pages"
                  v-model="addItem.noOfPages"
                ></v-text-field>
              </v-col>
            </v-row>
          </v-container>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="blue darken-1" text @click="dialogBoxFn()">
            Close
          </v-btn>
          <v-btn color="blue darken-1" text @click="save"> Save </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-row>
</template>
<script>
export default {
  name: "AddItem",
  data: () => ({
    dialog: false,
    addItem: {
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
    addIndex: -1,
    Books: [],
  }),
  props: {
    studentName: String,
    dialogBox: Boolean,
    editItemProp: Object,
    editIndexProp: Number,
  },
  computed: {
      formTitle () {
        return this.addIndex === -1 ? 'Add Book' : 'Edit Book'
      },
    },
  watch: {
    dialogBox(newValue) {
      this.dialog = newValue;
      console.log(this.editItemProp);
      this.addItem = this.editItemProp;
      this.addIndex = this.editIndexProp;
    },
  },

  methods: {
    close() {
      this.dialog = false;
      this.addItem = Object.assign({}, this.defaultItem);
      this.addIndex = -1;
      this.$emit("closeBook", this.dialog);
    },
    save() {
      console.log("In child component", this.addItem);
      this.$emit("addBookToList", this.addItem);
      this.close();
    },

    dialogBoxFn() {
      this.dialog = false;
      this.$emit("callDialog", this.dialog);
      this.close();
      console.log("dialog box on close: ", this.dialog);
    },
  },
};
</script>
