<template>
  <v-container>
 <v-card
    class="mx-auto"
    tile
  >
    <v-card-title>
      <v-text-field
        v-model="search"
        append-icon="search"
        label="Search"
        single-line
        hide-details
      ></v-text-field>
       <v-text-field
       v-model="input_value"
            label="add key"
            :value="input_value"
            solo
                         prepend-icon="lock"
          ></v-text-field>
          <v-btn @click="addKey()" :loading="add_btn_loading" class="mx-2" fab dark color="indigo">
      <v-icon dark>mdi-plus</v-icon>
    </v-btn>
          
    </v-card-title>
  <v-data-table v-if="allKeys"
    :headers="headers"
    :items="allKeys.edges"
    :items-per-page="80"
    :search="search"
    class="elevation-1"
  >
      <template v-slot:body="{ items }">
        <tbody>
          <tr v-for="item in items" :key="item.node.name">
            <td>
                     <v-btn class="mx-2" @click="deleteKey(item.node.name)" fab :loading="remove_btn_loading" dark color="indigo">
      <v-icon dark>mdi-minus</v-icon>
    </v-btn>
            </td>
            <td>{{ item.node.id }}</td>
            <td>{{ item.node.name }}</td>
             <td>{{ item.node.value}}</td>
               <td>{{ item.node.createdAt}}</td>
          </tr>
        </tbody>
      </template>
  </v-data-table>
  </v-card>  
  </v-container>
</template>

<script>
import gql from 'graphql-tag'

var QUERY = gql`
    query{
  allKeys{
    edges{
      node{
        id
        name
        value
        createdAt
      }
    }
  }
}`;

// var CREATE_MUTATION = ;

  export default {
    name: 'Keys',
    apollo: {
  },
    data: () => ({
      allKeys:{},
      add_btn_loading:false,
      remove_btn_loading:false,
       input_value:'',
        search: '',
        headers: [
            { text: 'Actions'
            },
          {
            text: 'KeyId',
            align: 'start',
            sortable: true,
            value: 'name',
          },
          { text: 'Name', 
          value: 'name',
          sortable: true
          },
          { text: 'Value',
           value: 'value',
           sortable: true
            },
            { text: 'Created At',
           value: 'created_at',
           sortable: true
            }
        ],
      keys: [
        
      ]
    }),
    created() {
      this.viewKeys();
    },
    methods: {
  viewKeys(){
this.$apollo.query({
        query:QUERY
      }).then(( response) =>{
         this.$nextTick(()=>{
        this.allKeys = response.data.allKeys;
         });
      });
  },
  async deleteKey(name){
    this.$apollo.mutate({
mutation:gql`
mutation($name:String){
  deleteKey(name:$name){
    ok
  }
}
`, 
variables:{
       name:name
     }
    }).then(() =>{
      this.hardReload();
    })
  },
  //Enables hard system reload. 
  hardReload(){
    var temp_wind = window.location.href;
      window.location.href = temp_wind;
  },
  async addKey() {
    this.add_btn_loading = true;
    // Call to the graphql mutation
     this.$apollo.mutate({
      // Query
      mutation: gql`mutation($name:String!){
  createKey(name:$name){
    ok
    key{
      name
    }
  }
}`,
      // Parameters
      variables: {
        name: this.input_value,
      },
    }).then(() =>{
      this.viewKeys();
      this.hardReload();
      this.add_btn_loading = false;
    }).catch(()=>{
         this.add_btn_loading = false;
    })
  }
}
  }
</script>
