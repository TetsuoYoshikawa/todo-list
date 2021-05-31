<template>
  <div>
    <div class="card">
      <h1>Todo List</h1>
      <div class="form">
        <div class="new">
          <input type="text" v-model="content">
          <button class="add" @click="insertTodo">追加</button>
        </div>
        <div class="lists" v-for="item in contents" :key="item.id">
          <input type="text" v-model="item.content">
          <div class="button">
            <button class="update" @click="updateTodo(item.id, item.content)">更新</button>
            <button class="delete" @click="deleteTodo(item.id)">削除</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      content: "",
      contents: [],
    };
  },
  methods: {
    async getTodo() {
      const resData = await axios.get("https://quiet-oasis-59544.herokuapp.com/api/todos");
      this.contacts = resData.data.data;
    },
    async insertTodo() {
      const sendData = {
        todo: this.newTodo,
      };
      await axios.post("https://quiet-oasis-59544.herokuapp.com/api/todos", sendData);
      await this.getTodo();
    },
    async updateTodo(id, todo) {
      const sendData = {
        todo:todo,
      };
      await axios.put("https://quiet-oasis-59544.herokuapp.com/api/todos/" + id, sendData);
      await this.getTodo();
    },
    async deleteTodo(id) {
      await axios.delete("https://quiet-oasis-59544.herokuapp.com/api/todos/" + id);
      await this.getTodo();
    },
  },
  created() {
    this.getTodo();
  },
};
  
</script>
    
<style>
html, body, div, span, object, iframe,
h1, h2, h3, h4, h5, h6, p, blockquote, pre,
abbr, address, cite, code,
del, dfn, em, img, ins, kbd, q, samp,
small, strong, sub, sup, var,
b, i,
dl, dt, dd, ol, ul, li,
fieldset, form, label, legend,
table, caption, tbody, tfoot, thead, tr, th, td,
article, aside, canvas, details, figcaption, figure,
footer, header, hgroup, menu, nav, section, summary,
time, mark, audio, video {
    margin:0;
    padding:0;
    border:0;
    outline:0;
    font-size:100%;
    vertical-align:baseline;
    background:transparent;
}
body {
    line-height:1;
}
article,aside,details,figcaption,figure,
footer,header,hgroup,menu,nav,section {
    display:block;
}
nav ul {
    list-style:none;
}
blockquote, q {
    quotes:none;
}
blockquote:before, blockquote:after,
q:before, q:after {
    content:'';
    content:none;
}
a {
    margin:0;
    padding:0;
    font-size:100%;
    vertical-align:baseline;
    background:transparent;
}
/* change colours to suit your needs */
ins {
    background-color:#ff9;
    color:#000;
    text-decoration:none;
}
/* change colours to suit your needs */
mark {
    background-color:#ff9;
    color:#000;
    font-style:italic;
    font-weight:bold;
}
del {
    text-decoration: line-through;
}
abbr[title], dfn[title] {
    border-bottom:1px dotted;
    cursor:help;
}
table {
    border-collapse:collapse;
    border-spacing:0;
}
/* change border colour to suit your needs */
hr {
    display:block;
    height:1px;
    border:0;  
    border-top:1px solid #cccccc;
    margin:1em 0;
    padding:0;
}
input, select {
    vertical-align:middle;
    color:#000;
}
html {
  background-color: #2d197c;
}
* {
  font-family: "Noto Sans JP";
}
.card {
  margin: 300px auto;
  width: 500px;
  background: #fff;
  border-radius: 5px;
  padding: 20px;
}
.card h1 {
  color: black;
  font-size: 1.5rem;
}
.new {
  display: flex;
  justify-content: space-between;
  margin-top: 15px;
}
.new input {
  display: block;
  width: 60%;
  padding: 5px;
  border-radius: 5px;
  border: 1px solid #ccc;
  font-size: 14px;
  margin-right: 10px;
}
.lists {
  display: flex;
  justify-content: space-between; 
  margin-top: 15px;
}
.lists input {
  display: block;
  width: 30%;
  padding: 5px;
  border-radius: 5px;
  border: 1px solid #ccc;
  font-size: 14px;
  margin-right: 10px;
}
.form {
  text-align: center;
}
.add {
  text-align: left;
  border: 2px solid #dc70fa;
  font-size: 12px;
  color: #dc70fa;
  background-color: #fff;
  font-weight: bold;
  padding: 8px 16px;
  border-radius: 5px;
  cursor: pointer;
  transition: 0.5s;
  height: 2.2rem;
}
.add:hover {
  background-color: #dc70fa;
  color: #fff;
}
.update {
  text-align: left;
  border: 2px solid #fa9770;
  font-size: 12px;
  color: #fa9770;
  background-color: #fff;
  font-weight: bold;
  padding: 8px 16px;
  border-radius: 5px;
  cursor: pointer;
  transition: 0.4s;
  outline: none;
  margin-right: 5px;
}
.update:hover {
  background-color: #fa9770;
  color: #fff;
}
.delete {
  text-align: left;
  border: 2px solid #71fadc;
  font-size: 12px;
  color: #71fadc;
  background-color: #fff;
  font-weight: bold;
  padding: 8px 16px;
  border-radius: 5px;
  cursor: pointer;
  transition: 0.4s;
  outline: none;
}
.delete:hover {
  background-color: #71fadc;
  color: #fff;
}
</style>
