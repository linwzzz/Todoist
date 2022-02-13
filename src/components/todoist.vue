<template>
  <div class="todoist">
    <h1>TODOLIST</h1>
    <div class="input">
      <input type="text" v-model="newTodo" @keyup.enter="inputHandler" />
      <button type="submit" @click="inputHandler" >
        送出
      </button>
      <button type="submit" @click="cencelHandler">取消</button>
    </div>
    <div class="list" v-for="(item, index) in todo" :key="index">
      <div class="txt" :class="[item.completed ? completed : '']">
        <p @click="completedHandler(index)">{{ item.title }}</p>
      </div>
      <div class="icon">
        <p @click="editHandler(index)">修改</p>
        <p @click="deleteHandler(index)">刪除</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data() {
    return {
      newTodo: "",
      editIndex:"",
      todo: [
        {
          title: "待辦事項1",
          completed: true,
        },
        {
          title: "待辦事項2",
          completed: true,
        },
      ],
    };
  },
  methods: {
    inputHandler() {
      let addtodo = this.newTodo.trim();
      if (this.editIndex === "") {
        if (!addtodo) {
          alert("請輸入待辦事項！");
        } else {
          this.todo.push({
            title: addtodo,
            completed: false,
          });
        }
      }
      else{
        this.todo[this.editIndex].title=addtodo
      }
      this.newTodo = "";
      this.editIndex= "";
    },
    cencelHandler() {
      this.newTodo = "";
      this.editIndex= "";
    },
    editHandler(index) {
      this.newTodo = this.todo[index].title;
      this.editIndex = index;
    },
    deleteHandler(index) {
      this.todo.splice(index, 1);
      this.cencelHandler()
    },
    completedHandler(index){
      this.todo[index].completed = true;
    }
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.todoist {
  width: 500px;
  margin: 0 auto;
  background: #e3ae3c;
  /* min-height: 600px; */
  padding: 20px;
  border-radius: 25px;
  box-shadow: 8px 5px 5px rgba(0, 0, 0, 0.2);
}
h1 {
  font-size: 36px;
  font-weight: bold;
}
.input {
  /* background: azure; */
  margin: 20px 10px;
  display: flex;
  justify-content: space-around;
}
.input input {
  padding: 10px 5px;
  font-size: 20px;
  font-weight: bold;
  border: none;
  width: 60%;
}
.input button {
  width: 15%;
  border: none;
  font-size: 20px;
  font-weight: bold;
  background: #4a7d90;
  cursor: pointer;
}
.input button:nth-child(3) {
  background: #6b6b6b;
  cursor: pointer;
}
.list {
  display: flex;
  background: #939249;
  margin: 10px;
  justify-content: space-between;
  align-items: center;
  border-radius: 10px;
  padding: 0px 10px;
  box-shadow: 5px 3px 2px 1px rgba(0, 0, 0, 0.2);
}
.txt {
  font-size: 20px;
  font-weight: bold;
  cursor: pointer;
}
.icon {
  display: flex;
  font-size: 14px;
  font-weight: bold;
}
.icon p {
  padding: 10px 5px;
  border-radius: 50%;
  margin: auto 5px;
  cursor: pointer;
}
.icon p:first-child {
  background: #eab57f;
}
.icon p:last-child {
  background: #c24f1a;
}
.completed{
  text-decoration: black;
  background: black;
}
</style>
