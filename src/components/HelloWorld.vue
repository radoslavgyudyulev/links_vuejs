<template>
  <div class="hello">
    <div class="left">
      <h1>{{ title }}</h1>

      <form @submit.prevent="addLink">
        <input class="link-input" type="text" v-model="newLink" placeholder="Add a Link">
      </form>

      <ul>
        <li v-for="(link, index) in links" v-bind:key="index">
            {{ link }}
            <button v-on:click="removeLinks(index)" class="rm">Remove</button>
            <a v-on:click="removeLinks(index)" class="visit">Visit</a>
        </li>
      </ul>
    </div>
    <div class="right">
      <Stats />
    </div>
  </div>
</template>

<script>
import { mapState, mapMutations, mapActions } from 'vuex'
import Stats from './Stats';

export default {
  name: 'HelloWorld',
  data() {
    return {
      newLink: ''
    }
  },
  components: {
    Stats
  },
  computed: {
    ...mapState([
    'title',
    'links'
  ])
  },
  methods: {
    ...mapMutations([
      'ADD_LINK'
    ]),
    ...mapActions([                  
      'removeLink'
    ]),
    addLink: function() {
      this.ADD_LINK(this.newLink)
      this.newLink = '';
    },
    removeLinks: function(link) {    
      this.removeLink(link)
    }
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
html, #app, .home {
    height: 100%;
  }
  body {
    background-color: #F4F4F4;
    margin: 0;
    height: 100%;
  }

  .hello {
    display: grid;
    grid-template-columns: repeat(2, 50%);
    grid-template-rows: 100%;
    grid-template-areas:
      "left right";
    height: 100%;
  }

  .left, .right {
    padding: 30px;
  }

  ul {
    list-style-type: none;
    padding: 0;
  }
  ul li {
    padding: 20px;
    background: white;
    margin-bottom: 8px;
    border: 2px solid #444;
  }

  .right {
    grid-area: right;
    background-color: #E9E9E9;
  }

  input {
    border: none;
    padding: 20px;
    width: calc(100% - 40px);
    box-shadow: 0 5px 5px lightgrey;
    margin-bottom: 50px;
    outline: none;
  }

   .rm {
    float: right;
    text-transform: uppercase;
    font-size: .8em;
    background: #f9d0e3;
    border: none;
    padding: 5px;
    color: #ff0076;
    cursor:pointer;
  }

  .visit {
    float: right;
    margin-right: 5px;
    text-transform: uppercase;
    font-size: .8em;
    background: #bbd2f7;
    border: none;
    padding: 5px;
    color: #4286f4;
    cursor:pointer;
  }

</style>
