<template>
  <div class="container">
    <div class="large-12 medium-12 small-12 cell">
      <label>File
        <input type="file" id="file" ref="file" v-on:change="handleFileUpload()"/>
      </label>
        <button v-on:click="submitFile()">Submit</button>
        <button @click="getTest()">get</button>
    </div>
  </div>
</template>

<script>

  import axios from 'axios';      
  //import jQuery from 'jquery'
  
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
      getTest(){
        console.dir("dsfsd");
        axios.get('https://witty-pig-71.localtunnel.me/api/test')
        .then(function (response) {
          console.log(response);
        })
        .catch(function (error) {
          console.log(error);
        });
      },
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
        //formData.append('file', this.file);
        let medias = new Array({'post_detail_id' : 27, 'media_type' : 1, 'media_file' : 'gddfgf'});

        console.log(this.file);
        // var medias = new Array();
        // medias[0]['post_detail_id'] = 3106;
        // medias[0][media_type] = 1;
        // medias[0][media_file] = formData;

        /*
          Make the request to the POST /single-file URL
        */
        //axios.defaults.headers.common['Authorization'] = AUTH_TOKEN;
        let token = 'eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOjEsImlzcyI6Imh0dHA6Ly90YXNrZXItcHJldmlldy5jb20vYXBpL2F1dGgiLCJpYXQiOjE1MTkwMjk5NDIsImV4cCI6MzI2MDg1Mzk0MiwibmJmIjoxNTE5MDI5OTQyLCJqdGkiOiJzS1QzejU4enlxY21iNGs1In0.scgCrY7FQudwOEwKPCp2JxXm9PxfIG2gfJGZ2Av0Xog';

        axios.post( 'http://tasker-preview.com/api/upload_media_v2',
          {
              headers: {
                //'Content-Type': 'multipart/form-data',
                'Authorization': "bearer" + token,
              },
              data: JSON.stringify({
                  'medias' : medias
              }),
              //crossdomain: true,

          }
        ).then(response => {
                    console.log(response.data);                    
                    console.log("success");
                    //location.reload();
                })
          .catch(e => {
              console.log(e.response);              
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
