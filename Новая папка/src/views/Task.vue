<template>
  <div class="main">
    <sidebar/>
    <div class="main__container">
      <div class="main__tasks">
        <div v-for="(item, index) in arr" :key="index" class="main__task">

          <h3>{{ item.title }}</h3>
          <p>{{ item.deadline }}</p>
          <p v-for="item in item.tags">
            {{ item }}
          </p>
          <p>{{ item.date }}</p>
        </div>
      </div>
      <div class="main__form">
        <h3>Добавить новую задачу</h3>
        <input placeholder="Введите задачу" class="main__title" v-model="tasks.title" type="text">
        <input type="date" v-model="tasks.deadline">
        <div class="main__tag">
          <input placeholder="Введите подзадачу" v-model="tag" type="text">
          <button @click="addTag">+</button>
        </div>
        <div class="main__tags">
          <div v-for="(item,index) in tasks.tags" :key="index" class="main__item">
            <p>{{ item }}</p>
            <button @click="deleteTag(index)===index">-</button>
          </div>

        </div>
        <button @click="addTask" class="main__addTask">Добавить</button>
      </div>
    </div>


  </div>
</template>

<script>
import Sidebar from "@/components/sidebar"

export default {
  components: {
    Sidebar
  },
  data() {
    return {
      tag: '',
      tasks: {
        title: '',
        date: new Date(),
        deadline: '',
        tags: []
      },
      arr: [],
    }
  },
  methods: {
    printDate: function () {
      return new Date().toLocaleDateString();
    },
    addTask() {
      let arr = JSON.parse(localStorage.getItem('tasks'));
      arr.push(this.tasks)
      localStorage.setItem('tasks', JSON.stringify(arr));
    },
    addTag() {
      this.tasks.tags.push(this.tag)
    },
    deleteTag(index) {
      this.tasks.tags.splice(index, 1)
      this.tags.splice(index, 1);
    },
    tagsUpdate() {
      console.log(localStorage.getItem('tasks'))
      if (localStorage.getItem('tasks')) {
        this.arr = JSON.parse(localStorage.getItem("tasks"))

        console.log(this.arr);
      }
    }
  },
  computed: {},
  mounted() {
    // let arr = []
    // arr[0] = this.tasks
    // this.tasks.date = this.printDate();
    // localStorage.setItem('tasks',  JSON.stringify(arr));
    this.tagsUpdate();
  },

}
</script>

<style lang="scss" scoped>
.main {
  width: 100%;
  height: 100vh;

  display: flex;

  &__container {
    width: 100%;
    display: flex;
    justify-content: space-between;
  }

  &__tasks {
    width: 100%;
    display: flex;
    align-items: start;

    flex-wrap: wrap;

  }
  &__task {
    width:200px;
    height: 200px;
    padding: 10px 20px;
    background: #ccc;


    border-radius: 20px;
    margin: 10px 20px;
  }

  &__form {
    width: 25%;
    height: 100%;
    position: relative;
    background: #000;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;


    padding: 0 20px;
  }

  &__form input, p {
    margin-bottom: 20px;
  }

  &__tag {
    position: relative;
  }

  &__form input {
    width: 80%;
    height: 40px;

    padding: 0 20px;
    font-size: 14px;
    color: #fff;

    background: #1f1d1d;

    user-select: none;

    outline: none;

    border: none;
    border-radius: 20px;


  }

  &__tag button {
    position: absolute;
    top: 10px;
    right: 10px;

    color: #fff;

    background: black;

    border-radius: 20px;

    cursor: pointer;

    outline: none;
  }

  &__form p {
    color: #fff;
    text-align: center;
  }

  &__addTask {
    width: 80%;
    height: 40px;

    background: #1f1d1d;
    position: absolute;
    bottom: 10px;

    font-size: 14px;
    color: #fff;

    border-radius: 20px;

    transition: .4s;

  }

  &__addTask:hover {
    background: #fff;
    color: #000;
  }

  &__item {
    width: 100%;
    display: flex;
    padding-right: 25px;
    position: relative;
  }


  &__item button {
    width: 20px;
    height: 20px;

    display: flex;
    align-items: center;
    justify-content: center;

    position: absolute;
    right: 0;
    top: 0;

    border: none;
    background: #1f1d1d;

    color: #fff;
    font-size: 20px;

    border-radius: 50px;

    cursor: pointer;

  }

}


</style>
