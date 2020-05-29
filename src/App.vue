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
    <ul v-for="(list, i) in lists" v-bind:key="i">
      <li>
        id: {{i}}, title: {{ list.title }}{{list.body}}
        <button @click="deleteList(i)">削除</button>
      </li>
    </ul>
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