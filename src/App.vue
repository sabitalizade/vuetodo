<script>
export default {
  name: "App",
  data(){
    return{
      value:'',
      datas:[]
    }
  },
  methods:{
    handleSave(e){
      e.preventDefault()
      if(this.datas.find(e=>e==this.value)|| this.value=="")return
      this.datas.push({ text:this.value,mark:false})
      this.value=''
      console.log(this.datas)
    },
    handleMarked(id){
      this.datas[id].mark=!this.datas[id].mark
    },
    handleDelete(item){
      this.datas=this.datas.filter(e=>e!==item)
    }

  }
};
</script>

<template>
  <div id="app">
    <div class="writingArea">
      <form>
        <input
          class="inputTitle"
          type="text"
          placeholder="Your todos"
          v-model="value"
        >
        <button class="submitButton" @keypress.enter="handleSave" @click="handleSave">Save</button>
      </form>
    </div>
    <div class="noteList">
      <ul>
        <li v-for="(item,id) in datas" :key="item.id"  >
          <span v-bind:class="{marked:item.mark}">
          {{ item.text }}

          </span>
          <div class="flex">
            <span class="mark" @click="handleMarked(id)">&#9745;</span> <button @click="handleDelete(item)">delete</button>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>



<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
 
  color: #2c3e50;
  margin: 60px;
}
* {
  color: aliceblue;
  text-decoration: none;
  list-style: none;
  box-sizing: border-box;
  outline: 0;
  padding: 0;
  margin: 0;
  font-size: 20px;
}
body {
  background-color: #0f0f1b;
}
.app {
  display: flex;
  max-width: 1400px;
  width: 100%;
  flex-direction: column;
  align-items: center;
}
.noteList {
  width: 80vw;
  min-height: 100vh;
}
.noteList ul {
  padding: 0;
  margin: 0;
}
.noteList ul li {
  width: 100%;
  padding: 10px 0 10px 25px;
  cursor: pointer;
  transition: 300ms all;
  word-wrap: break-word;
  position: relative;
  box-sizing: border-box;
}
.noteList ul li button {
  background: red;
  font-size: 12px;
  padding: 10px 15px;

  border: 0;
  border-radius: 5px;
}
.flex {
  position: absolute;
  right: 0;
  top: 0px;
  display: flex;
}
.marked {
  text-decoration: line-through;
}
.mark {
  background: green;
  font-size: 15px;
  padding: 10px 15px;
  border: 0;
  border-radius: 5px;
  margin-right: 3px;
}
.noteList ul li:hover {
  background: rgba(1, 42, 74, 1.8);
}
.writingArea {
  display: flex;
  flex-direction: column;
  position: relative;
}
.writingArea .inputTitle {
  width: 80vw;
  border: none;
  height: 50px;
  background-color: #171727;
  border-bottom: black 1px solid;
  padding-left: 10px;
  word-wrap: break-word;
  border-radius: 5px;
  margin-top: 5px;
}

.writingArea .submitButton {
  padding: 12px 35px;
  text-align: center;
  position: absolute;
  border-radius: 5px;
  background: firebrick;
  top: 0;
  right: 0;
  border: none;
  cursor: pointer;
  margin-top: 5px;
}
/* .writingArea textarea{
min-height: calc(100vh - 50px);
color: rgb(218, 218, 218);
  border: none;
  background: #171727;
  padding-left: 10px;

} */
</style>
