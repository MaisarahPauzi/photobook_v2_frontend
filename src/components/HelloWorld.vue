<template>
  <v-container grid-list-xl>
    <v-layout align-center justify-center v-for="item of items">
      <v-flex xs12 sm8 md6>
        <v-card>
          <v-img
              v-bind:src="img_src+item.filename" 
              aspect-ratio="1"
            ></v-img>

            <v-card-title primary-title>
              <div>
                <h3 class="headline mb-0">{{item.title}}</h3>
                <p>{{item.caption}}</p>
              </div>
            </v-card-title>
            <v-card-actions>
                  <v-spacer></v-spacer>
                  <Popup :id="item.id" :title="item.title" :caption="item.caption" :filename="item.filename"></Popup>
                  
                  <v-btn  color="error" @click="deleteData(item,index)">
                    <v-icon>delete</v-icon>DELETE
                  </v-btn>
            </v-card-actions>
        </v-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
import axios from 'axios';
import Popup from './Popup';
export default {
  name: 'HelloWorld',
  components:{
      Popup,
    },
  data () {
    return {
      img_src:'http://52.40.179.3/DemoProject/public/storage/',
      items:[],
    }
  },
  
  created() {

    axios.get(`http://52.40.179.3/DemoProject/public/api/photobook`)
    .then(response => {
      // JSON responses are automatically parsed.
      this.items = response.data
    })
    .catch(e => {
      this.errors.push(e)
    });
    
  },

  methods:{
    deleteData(item,index){
        axios.delete( 'http://52.40.179.3/DemoProject/public/api/photobook/'+item.id
            ).then(function(){
          console.log('success');
        })
        .catch(function(){
          console.log('failed');
        });

        axios.delete( 'http://52.40.179.3/DemoProject/public/api/delPhoto/'+item.filename
            ).then(function(){
          console.log('success delete file');
        })
        .catch(function(){
          console.log('failed');
        });

        this.items.splice(index,1);
      }
  }


}

</script>

<style>

</style>
