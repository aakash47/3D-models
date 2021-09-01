<template>
<div>
    <form class="example" @click.prevent="search" style="margin:auto;max-width:300px">
    <input type="text" v-model="searchs" placeholder="Search.." name="search2">
    <button type="submit"><i class="fa fa-search"></i></button>
    </form>
 <div>
<iframe class="container"  id="api-frame" allow="autoplay; fullscreen; vr" allowvr allowfullscreen mozallowfullscreen="true" webkitallowfullscreen="true"></iframe>
</div>
</div>
</template>
<script>
import axios from 'axios'
export default {
    name:"Iframe",
    data(){
        return {
            searchs:"",
        }},
        methods:{
            async search(){
            const access_token=''

                const {data} = await axios.get(`https://api.sketchfab.com/v3/search?type=models&q=%20${this.searchs}`, {
            headers: {
            'Authorization': `token ${access_token}`
            }})
            console.log(data.results);

            console.log(data.results[0].uid);
            this.skr=data.results[0].uid;
        var iframe = document.getElementById( 'api-frame' );
        var client = new window.Sketchfab( iframe );
        console.log(iframe)
        client.init( this.skr, {
        success: function onSuccess( api ){
            api.start();
            api.addEventListener( 'viewerready', function() {
                console.log( 'Viewer is ready' );
            } );
        },
        error: function onError() {
            console.log( 'Viewer error' );
        }
    } );
        }   
}            
        }    
</script>

<style scoped>
@import "https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css";

* {
  box-sizing: border-box;
}
.container {
    margin-top:15px;
    width:98vw;
    height:88vh;
    border-radius:15px;
    }
form.example input[type=text] {
  padding: 10px;
  font-size: 17px;
  border: 1px solid grey;
  float: left;
  width: 80%;
  background: #f1f1f1;
}

form.example button {
  float: left;
  width: 20%;
  padding: 10px;
  background: #2196F3;
  color: white;
  font-size: 17px;
  border: 1px solid grey;
  border-left: none;
  cursor: pointer;
}

form.example button:hover {
  background: #0b7dda;
}

form.example::after {
  content: "";
  clear: both;
  display: table;
}
</style>
