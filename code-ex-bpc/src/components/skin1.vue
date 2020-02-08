<template>
  <div class="hello">
    <br>
    <div class="autosearch">
        <input v-model="query" v-on:keyup="autocomplete" type="text">
      <div class="suggestions">
        <div v-bind:key="index" v-for="(item,index) in results" v-bind:class="{'auto-item':true, 'active':(index === focus)}">
          <strong>{{ item.name }}</strong>
          <br>
          {{ item.description }}
          <br>
          <div class="tag" v-bind:key="index" v-for="(tag,index) in item.tags">
            <button>#{{ tag }}</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

import axios from "axios";

export default {
  name: 'skin1',
  data () {
    return {
      query: "",
      results: [],
      focus: -1,
      length: 0,
      populate: "",
    }
  },
  methods: {
    autocomplete: function(event) {
      
      // highlight the appropriate autocomplete-item
      if (event.keyCode === 40 ) {
        if(this.focus < (this.length-1)) {
          this.focus++;
        }
        else {
          this.focus = 0;
        }
      }
      else if (event.keyCode === 38) {
        if(this.focus > -1) {
          this.focus--;
        }
        else {
          this.focus = (this.length -1)
        }
      }
      else if (event.keyCode === 13) {
        // if user presses enter on highlighted item, populate search bar with the name
        this.query = this.results[this.focus].name;
        this.results = [];
      }
      else {
        axios({ method:"GET", url:this.query, baseURL:"https://coding-challenge.echoandapex.com/locations?q="}).then(result => {
        this.results = result.data.predictions;
        this.length = result.data.predictions.length;
        this.focus = -1;
      }, 
      )
      }
    },
   },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.suggestions {
  overflow: hidden; 
  width: 350px;
  position: relative;
  border: 1px solid transparent;
  border-top: none;
  border-bottom: none;
  border-radius: 0px 0px 25px 25px;
}

.auto-item {
  text-align: left;
  background-color: white;
  top: 100%;
  padding: 10px;
  width: 100%;
  left: 0;
  right: 0;
  border-top: 1px solid gray;
}

.active {
  background-color: grey;
}

input {
  width: 350px;
  font-size: 16px;
  padding-bottom: 10px;
}

.hello {
  text-align: center;
}

.autosearch {
  position: relative;
  display: inline-block;
}

button {
  background-color: lightgrey;
  padding: 10px 20px;
  text-align: center;
  display: inline-block;
  border-radius: 16px;
  position: relative;
  margin: 5px;
}
.tag {
  display: inline-block;
};
</style>
