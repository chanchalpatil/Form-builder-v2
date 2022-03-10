<template>
<div class="row">

  <!-- column-1 -->
  <div class="col mx-2 px-2 py-3 shadow bg-light border rounded">
    <h1> Form Attributes </h1>
  <!--button-->
    <button class="btn btn-secondary button" @click="text()">Text</button>
    <button class="btn btn-secondary button" @click="multiline()"> Multiline </button>
    <button class="btn btn-secondary button" @click="checkbox()"> Checkbox </button><br>
    <button class="btn btn-secondary button" @click="submit()"> Submit </button>
  </div>

  <!-- column-2 -->
  <div class="col mx-2 px-2 py-3 shadow bg-light border rounded">
    <h1> Form </h1>
    <draggable class="draggable-list" :list="List" group="List">
      <!--loop-->
      <div v-for="(idx, index) in List" :key="idx.type">
        <!-- text -->
        <div v-if="idx.type==='text'">
          <div class="bg-white mt-3 p-2 shadow border rounded">
            <button type="button" class="btn btn-secondary pull-right" aria-label="Close" @click="removeAt(index)" >
            <span aria-hidden="true">×</span>
            </button>
            <p>Message is: {{ message1 }}</p>
            <input v-model="message1" placeholder="edit me"/>
          </div>
        </div>
  
        <!-- multiline -->
        <div v-else-if="idx.type === 'multiline'">
          <div class="bg-white mt-3 p-2 shadow border rounded">
            <button type="button" class="btn btn-secondary pull-right" aria-label="Close" @click="removeAt(index)" >
            <span aria-hidden="true">×</span>
            </button>
            <span>Multiline message is:</span>
            <p style="white-space: pre-line;">{{ message2 }}</p>
            <textarea v-model="message2" placeholder="add multiple lines"></textarea>
          </div>
        </div>

        <!-- checkbox -->
        <div v-else-if="idx.type === 'checkbox'">
          <div class="bg-white mt-3 p-2 shadow border rounded">
            <button type="button" class="btn btn-secondary pull-right" aria-label="Close" @click="removeAt(index)" >
            <span aria-hidden="true">×</span>
            </button>
            <div>Checked names: {{ checkedNames }}</div>

              <input type="checkbox" id="x" value="x" v-model="checkedNames" />
              <label for="jack">Jack</label>
 
              <input type="checkbox" id="y" value="y" v-model="checkedNames" />
              <label for="john">John</label>
 
              <input type="checkbox" id="z" value="Mike" v-model="checkedNames" />
              <label for="mike">Mike</label>
          </div>
        </div>
        <div v-else-if="idx.type === 'submit'">
          <div class="bg-white mt-3 p-2 shadow border rounded">
            <input class="btn btn-secondary" type="submit" value="Submit">
            <button type="button" class="btn btn-secondary float-right" aria-label="Close" @click="removeAt(index)" >
            <span aria-hidden="true">×</span>
            </button>
          </div>
        </div>
      </div>
    </draggable>
  </div>

  <!-- column-3 -->
  <div class="col mx-2 px-2 py-3 shadow bg-light border rounded">
  <!-- display list -->
  <rawDisplayer :value="List" title="List" />
  </div>
  
</div>
</template>

<script>
let id = 0;
import rawDisplayer from "./components/rawDisplayer.vue";
import draggable from "vuedraggable";
export default {
  components:{
    rawDisplayer,
    draggable
  },
  data() {
    return {
      message1: '',
      message2: '',
      checkedNames: [],
      List:[],

    };
  },
  methods:{
    text: function(){
      id++;
      this.List.push({type: "text",id});
    },
    multiline: function(){
      id++;
      this.List.push({type: "multiline",id});
    },
    checkbox: function(){
      id++;
      this.List.push({type: "checkbox",id});
    },
    submit: function(){
      id++;
      this.List.push({type:"submit",id});
    },
    removeAt(index){
      this.List.splice(index,1);
    }

  }
};
</script>

<style scoped>
h6 {
  font-weight: 700;
}
.col {
  height: 90vh;
  overflow: auto;
}
.draggable-list {
  min-height: 10vh;
}
.draggable-list > div {
  cursor: pointer;
}
</style>