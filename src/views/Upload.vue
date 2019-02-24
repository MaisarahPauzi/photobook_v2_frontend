<template>
  <v-container grid-list-xl>
    <v-layout align-center justify-center>
      <v-flex xs12 sm6 md6>
        <v-card>
          <v-card-title primary-title>
              <div>
                <h3 class="headline mb-0">Upload Picture</h3>
              </div>
            </v-card-title>
            <div align="center">
                <input type="file" id="file" ref="file" v-on:change="handleFileUpload()"/>
                <v-text-field label="Title" placeholder="Insert title" box v-model="title"></v-text-field>
                <v-text-field label="Caption" placeholder="Insert caption" box v-model="caption"></v-text-field>
            </div>
            <div align="right">
              <v-btn color="info" v-on:click="submitData()">Submit</v-btn>
            </div>
            
        </v-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
import axios from 'axios';
export default {
  name: 'upload',
  data () {
    return {
      title:'',
      caption:'',
      img_src:'https://backendlessappcontent.com/D6E5A353-CD1B-1F0B-FF18-F4FCB3F3CF00/console/dzcfasxclleuwjnoxljtcwutqaoaqivsvizx/files/view/uploads/',
      images:[],
      file: '',
      items:[],
    }
  },
  
  created() {
  },

  methods:{
        submitData(){


        axios.post( 'http://54.191.107.199/DemoProject/public/api/photobook',
                {
                  "title":this.title,
                  "caption":this.caption,
                  "filename":this.file.name
                }
            ).then(function(){
          console.log('success');
        })
        .catch(function(){
          console.log('failed');
        });
        this.title = '';
        this.caption = '';
        this.file = '';
        
      },


      handleFileUpload(){
        this.file = this.$refs.file.files[0];
        
            let fileData = new FormData();

            fileData.append('file', this.file);


            axios.post( 'http://54.191.107.199/DemoProject/public/api/upload',
                fileData,
                {
                headers: {
                    'Content-Type': 'multipart/form-data'
                }
              }
            ).then(function(){
          console.log('success');
        })
        .catch(function(){
          console.log('failed');
        });
      

      }
  }
}

</script>

<style>

</style>
