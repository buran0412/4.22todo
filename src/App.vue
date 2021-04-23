<template>
  <div class="container">
    <div class="card">
      <p class="title todolist">Todo List</p>
      <div class="todo">
        <div class="flex between add">
          <input type="text" v-model="newTodo" class="input-add" />
          <button class="button-add" @click="addTodo">追加</button>
        </div>
        <div
          class="flex between updelete"
          v-for="todo in todoList"
          :key="todo.id"
        >
          <input type="text" class="input-update" v-model="todo.name" />
          <div>
            <button
              class="button-update"
              @click="updateTodo(todo.id, todo.name)"
            >
              更新
            </button>
            <button class="button-delete" @click="deleteTodo(todo.id)">
              削除
            </button>
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
      newTodo: "",
      todoList: [],
    };
  },
  methods: {
    async addTodo() {
      const sendData = {
        name: this.newTodo,
      };
      await axios.post("http://127.0.0.1:8000/api/todo/", sendData);
      this.getTodos();
      this.newTodo = "";
    },
    async updateTodo(id, name) {
      const sendData = {
        name: name,
      };
      await axios.put("http://127.0.0.1:8000/api/todo/" + id, sendData);
      this.getTodos();
    },
    async deleteTodo(id) {
      await axios.delete("http://127.0.0.1:8000/api/todo/" + id);
      this.getTodos();
    },
    async getTodos() {
      const getData = await axios.get("http://127.0.0.1:8000/api/todo/");
      this.todoList = getData.data.data;
    },
  },
  created() {
    this.getTodos();
  },
};
</script>

<style>
html,
body,
div,
span,
applet,
object,
iframe,
h1,
h2,
h3,
h4,
h5,
h6,
p,
blockquote,
pre,
a,
abbr,
acronym,
address,
big,
cite,
code,
del,
dfn,
em,
img,
ins,
kbd,
q,
s,
samp,
small,
strike,
strong,
sub,
sup,
tt,
var,
b,
u,
i,
center,
dl,
dt,
dd,
ol,
ul,
li,
fieldset,
form,
label,
legend,
table,
caption,
tbody,
tfoot,
thead,
tr,
th,
td,
article,
aside,
canvas,
details,
embed,
figure,
figcaption,
footer,
header,
hgroup,
menu,
nav,
output,
ruby,
section,
summary,
time,
mark,
audio,
video {
  margin: 0;
  padding: 0;
  border: 0;
  font-size: 100%;
  font: inherit;
  vertical-align: baseline;
}
/* HTML5 display-role reset for older browsers */
article,
aside,
details,
figcaption,
figure,
footer,
header,
hgroup,
menu,
nav,
section {
  display: block;
}
body {
  line-height: 1;
}
ol,
ul {
  list-style: none;
}
blockquote,
q {
  quotes: none;
}
blockquote:before,
blockquote:after,
q:before,
q:after {
  content: "";
  content: none;
}
table {
  border-collapse: collapse;
  border-spacing: 0;
}
.container {
  background-color: #2d197c;
  height: 100vh;
  width: 100vw;
  position: relative;
}
.card {
  background-color: #fff;
  width: 50vw;
  padding: 30px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  border-radius: 10px;
  font-weight: bold;
  font-size: 24px;
}
.input-add {
  width: 80%;
  padding: 5px;
  border-radius: 5px;
  border: 2px solid #ccc;
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
  font-size: 14px;
  outline: none;
  vertical-align: middle;
}
.button-add {
  text-align: left;
  border: 2px solid #dc70fa;
  font-size: 12px;
  color: #dc70fa;
  background-color: #fff;
  font-weight: bold;
  padding: 8px 16px;
  border-radius: 5px;
  cursor: pointer;
  transition: 0.4s;
  outline: none;
}
.input-update {
  width: 80%;
  padding: 5px;
  border-radius: 5px;
  border: 1px solid #ccc;
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
  font-size: 14px;
  outline: none;
  vertical-align: middle;
}
.todolist {
  margin: 0;
  padding: 0;
  border: 0;
  outline: 0;
  font-size: 100%;
  vertical-align: baseline;
  background: transparent;
}
.button-update {
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
}
.button-delete {
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
</style>
