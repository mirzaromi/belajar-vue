<script setup>
import { reactive, ref, computed } from "vue";
import MyComponents from "./components/MyComponents.vue"
// import func from "../vue-temp/vue-editor-bridge";
const state = reactive({
  count: 0,
  title: 'Halo ini judulnya',
  show : true,
  x : 0,
  y : 0,
  showBooks: true,
  books : [
    { title: 'ini judul ke 1', author: 'ini author ke 1', img:'/assets/balik pondok.png', isFav:true},
    { title: 'ini judul ke 2', author: 'ini author ke 2', img:'/assets/brosur.jpeg', isFav:false},
    { title: 'ini judul ke 3', author: 'ini author ke 3', img:'/assets/brosur2.jpeg', isFav:true},
  ],
  name: "ini nama propsnya",
  text: "ini text props nya",
  theme: "custom",
  modalShow: false,
});

function increment() {
  state.count++;
}

function decrement() {
  state.count--;
}

function changeTitle() {
  state.title = "judul berubah";
}

function showOrHide() {
  state.show == true ? state.show = false : state.show = true; 
}

function toggleFav(book) {
  book.isFav = !book.isFav
}

function handleEvent(e) {
  state.x = e.offsetX
  state.y = e.offsetY
}

function showModal() {
  state.showModal = !state.showModal
}

const filterBooks = computed(() => {
  return state.books.filter((book) => book.isFav)
})
</script>

<template>
<div v-if="state.showModal">
  <MyComponents :name="state.name" :text="state.text" :theme="state.theme" @close="showModal"/>
</div>
<button @click="showModal">show modal</button>
  <div v-if="state.show">
  <h1>{{ state.title }}</h1>
  <h1>{{ state.count }}</h1>
  </div>

  <button @click="increment">increase</button>
  <button @click="decrement">decrease</button>
  <button @click="changeTitle">Ubah Judul</button>

  <br>
  <br>
  <button @click="showOrHide">
    <span v-if="state.show">Hide</span>
    <span v-else>Show</span>
  </button>

  <span v-show="state.show">Muncul</span>

  <br>
  <br>
  <div class="box" @mousemove="handleEvent">Position - X : {{state.x}} Y : {{state.y}}</div>


  <div v-if="state.showBooks">
    <ul>
      <li v-for="book in filterBooks" :key="book" :class="{fav: book.isFav}" @click="toggleFav(book)">
        <h4>{{ book.title }}</h4>
        <h6>{{ book.author }}</h6>
        <img :src="book.img" alt="">
      </li>
    </ul>
  </div>
</template>

<style>
  body{

    margin: 20px auto;
  }
  p, h4, h6, ul {
    margin: 0;
    padding: 0;
  }
  li {
    list-style-type: none;
    background: #ddd;
    margin: 20px auto;
    padding: 10px 20px;
    border-radius: 20px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    color: #000;
  }
  li img {
    width: 150px;
  }
  .box{
    width: 400px;
    height: 200px;
    background-color: #ddd;
    color: #000;
  }

  li.fav {
    background: rgb(106, 201, 161);
  }
</style>