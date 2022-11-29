<template>
  <v-data-table
      :headers="headers"
      :items="userData"
      sort-by="id"
      class="elevation-1"
    >
  </v-data-table>
</template>
<script>
import axios from 'axios';
export default {
  name: "DataDisplay",
  data() {
    return {
      headers: [
          {
            text: 'User ID',
            align: 'start',
            sortable: false,
            value: 'id',
          },
          { text: 'Name', value: 'name' },
          { text: 'Email Address', value: 'email' },
          { text: 'Username', value: 'username'},
          { text: 'City', value: 'address.city'},
          { text: 'Zipcode', value:'address.zipcode' }
        ],  
      userData: [],
    };
  },
   async created(){
        await this.get().then((resopnse)=>{
          this.userData = resopnse.data;
        });
    },
    methods:{
          get(){
            return axios.get("https://jsonplaceholder.typicode.com/users")
          }
    }
};
</script>
