<script setup>

import {ref, reactive, computed} from 'vue';
//import HelloWorld from './components/HelloWorld.vue'
import BooksComp from './components/BooksComp.vue';
import ProgressComp from './components/ProgressComp.vue';
import ProgressTagComp from './components/ProgressTagComp.vue';
import AddBookComp from './components/AddBookComp.vue';

  let books = reactive([
      {
        id: 1,
        title: "History of Europe",
        cover:
          "https://printpress.cmsmasters.net/default/wp-content/uploads/sites/11/2019/05/printpress-product-6-540x861.jpg",
        isRead: true,
        isbn: "0-395-07157-8",
        author: "Daniel Trejo",
      },
      {
        id: 2,
        title: "Penguin Classics",
        cover:
          "https://printpress.cmsmasters.net/default/wp-content/uploads/sites/11/2019/05/printpress-product-2-540x861.jpg",
        isRead: true,
        isbn: "0-395-07157-8",
        author: "Daniel Trejo, Jon Snow",
      },
      {
        id: 3,
        title: "Becoming",
        cover:
          "https://printpress.cmsmasters.net/default/wp-content/uploads/sites/11/2019/05/printpress-product-7-540x861.jpg",
        isRead: false,
        isbn: "0-395-07157-8",
        author: "Daniel Trejo",
      },
      {
        id: 4,
        title: "Sonnets",
        cover:
          "https://printpress.cmsmasters.net/default/wp-content/uploads/sites/11/2019/05/printpress-product-5-540x861.jpg",
        isRead: false,
        isbn: "0-395-07157-8",
        author: "Daniel Trejo",
      },
]);

const newId = computed(() => {
  let idInitial = books[0].id ? books[0].id : 0;

  if(books.length > 0) {
   for(let i = 0; i < books.length; i++) {
     if(idInitial < books[i].id) {
      idInitial = books[i].id;
     }
   }
  }

  idInitial++;
  return idInitial;
});

function bookIsRead(id) {
  console.log("emit ok", id);
 
  //1 forma de fazer
  books.filter((item) => {
    if(item.id == id) {
     item.isRead = !item.isRead;
    }
  });

  //2 forma
  // books.forEach((item) => {
  //   if(item.id == id) {
  //    item.isRead = !item.isRead;
  //   }
  // });

  //3 forma fazer com for(let i=0; i < length; i++)

  console.log(books);
}

let showAddBook = ref(false);

function closeAddBook() {
  console.log("Close Book");
  showAddBook.value = !showAddBook.value;
}

function addNewBook() {
  console.log("Add New Book");
  showAddBook.value = !showAddBook.value;
}

</script>

<template>
  
  <div v-if="!showAddBook" class="container">
    <h1>📖 Meus Livros</h1>
    <div class="header-btns">
      <button
        class="btn"
        @click="closeAddBook()"
      >
        Adicionar Livro +
      </button>
    </div>
 
    <div class="books-container">

      <BooksComp @bookIsRead="bookIsRead($event)"  :books="books"/>
      
      <ProgressComp :items="books"/>

      <br>
      <br>

      <ProgressTagComp :items="books"/>

    </div>
  </div>

  <div v-if="showAddBook" class="container">
    <AddBookComp @closeAddBook="closeAddBook()" @addNewBook="addNewBook()" :newId="newId"/>
  </div>

</template>

b
