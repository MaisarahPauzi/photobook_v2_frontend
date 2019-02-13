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
        </v-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
import axios from 'axios';
export default {
  name: 'HelloWorld',
  data () {
    return {
      img_src:'https://backendlessappcontent.com/D6E5A353-CD1B-1F0B-FF18-F4FCB3F3CF00/console/dzcfasxclleuwjnoxljtcwutqaoaqivsvizx/files/view/uploads/',
      items:[],
    }
  },
  
  created() {

    axios.get(`https://api.backendless.com/D6E5A353-CD1B-1F0B-FF18-F4FCB3F3CF00/24781313-4CE5-7BF9-FFC7-84519874BC00/data/storeimage`)
    .then(response => {
      // JSON responses are automatically parsed.
      this.items = response.data
    })
    .catch(e => {
      this.errors.push(e)
    });
    
  },


}

</script>

<style>

</style>
