<template>
  <div class="container">
    <div class="large-12 medium-12 small-12 cell">
      <label>File
        <input type="file" id="file" ref="file" v-on:change="handleFileUpload()"/>
      </label>
        <button v-on:click="submitFile()">Submit</button>
    </div>
  </div>
</template>

<script>

  import axios from 'axios';      

  
  export default {
    /*
      Defines the data used by the component
    */
    data(){
      return {
        file: ''
      }
    },

    methods: {
      /*
        Submits the file to the server
      */
      submitFile(){
        /*
            Initialize the form data
        */
        let formData = new FormData();

        /*
            Add the form data we need to submit
        */
        formData.append('file', this.file);
        let medias = new Array({'post_detail_id' : 3106, 'media_type' : 1, 'media_file' : formData});
        // var medias = new Array();
        // medias[0]['post_detail_id'] = 3106;
        // medias[0][media_type] = 1;
        // medias[0][media_file] = formData;

        /*
          Make the request to the POST /single-file URL
        */
        //axios.defaults.headers.common['Authorization'] = AUTH_TOKEN;
        let token = 'your_token';

        axios.post( '/url',
          {
              headers: {
                'Content-Type': 'multipart/form-data',
                'Authorization': "bearer" + token,
                'Access-Control-Allow-Origin': '*'
              },
              body: JSON.stringify({
                  'medias' : medias
              }),

          }
        ).then(function(data){
          console.log('SUCCESS!!');
          console.log(data);          
        })
        .catch(function(err){
          console.log('FAILURE!!');
          console.log(err);          
        });
      },

      /*
        Handles a change on the file upload
      */
      handleFileUpload(){
        this.file = this.$refs.file.files[0];
      }
    }
  }
</script>
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
