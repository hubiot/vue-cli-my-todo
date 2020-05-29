<template>
  <div id="app">
    <h1>MyTodoApp</h1>
    <div>
      <label>タイトル：</label>
      <!-- <label>タイトル：</label> -->
      <input type="text" v-model="title" placeholder="タイトル" />
    </div>
    <div>
      <label>内容：</label>
      <input type="text" v-model="body" placeholder="内容" />
    </div>
    <div>
      <input type="submit" value="追加" @click="addList" />
    </div>
    <div>
      <input type="submit" value="保存" @click="saveTodo" />
    </div>
    <table class="table" border="1">
      <thead>
        <tr>
          <th class="number">No</th>
          <th class="title">Title</th>
          <th class = "content">content</th>
          <th>del</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(list, i) in lists" v-bind:key="i">
          <td>{{i}}</td>
          <td><input type="text" v-model= "list.title" class="title_input" ></td>
          <td><input type="text" v-model= "list.body" class="content_input"></td>
          <td>
            <button @click="deleteList(i)">del</button>
          </td>
        </tr>
      </tbody>
    </table>
    <pre>
      {{$data}}
    </pre>
  </div>
</template>

<script>
export default {
  data: () => ({
    lists: [],
    title: "",
    body: ""
  }),
  methods: {
    // リストの追加
    addList: function() {
      if (this.title === "" || this.body === "") return;

      this.lists.push({ title: this.title, body: this.body });
      this.title = "";
      this.body = "";
    },
    // リストの削除
    deleteList: function(i) {
      this.lists.splice(i, 1);
    },
    //データをセーブ
    saveTodo: function() {
      localStorage.setItem("list_storage", JSON.stringify(this.lists));
    },
    loadTodo: function() {
      this.lists = JSON.parse(localStorage.getItem("list_storage"));
      if (!this.lists) {
        this.lists = [];
      }
    }
  },
  mounted: function() {
    this.loadTodo();
  }
};
</script>

<style>
.title_input[type="text"]
{
  border:none;
  outline:none;
  width:20px;
}
.title_input[type="text"]:focus
{
  border:1px solid #ff0000;
  outline:none;
  width:20px;
}
.content_input[type="text"]
{
  border:none;
  outline:none;
  width:250px;
}
.content_input[type="text"]:focus
{
  border:1px solid #ff0000;
  outline:none;
  width:200px;
}

table {
  border-collapse: collapse;
}
table th{
  border:sodid 1px black;
  background-color:#aaee5c;
}
table td{
  border:sodid 1px black;
}
.title
{
  width:20px;
}
.content
{
  width:250px;
}
</style>