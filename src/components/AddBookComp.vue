<script setup>

import {ref, reactive} from 'vue';

const emit = defineEmits(['closeAddBook','addNewBook']);

const props = defineProps(['newId']);

function closeAddBook() {
  emit('closeAddBook');
}

function addNewBook() {
  emit('addNewBook'
  /*, book*/);
}

let newBook = reactive(
      {
        id: props.newId,
        title: "",
        cover: "",
        isRead: false,
        isbn: "",
        author: "",
      }
    );

</script>

<template>

    <h1>📖 Adicionar Livro</h1>
    
    <div class="header-btns">
      <button class="btn" @click="closeAddBook()">
        Fechar x
      </button>
    </div>
 
    <form class="add-form">
       
        <div class="form-control">
        <label>Título <span>(ID - {{ newBook.id }})</span></label>
        <input
            type="text"
            name="text"
            placeholder="Adicione o título"
        />
        </div>
        <div class="form-control">
        <label>Capa</label>
        <input 
            type="text" 
            name="cover" 
            placeholder="Adicione o link da imagem de capa"
            />
        </div>
        <div class="form-control">
        <label>Autor</label>
        <input
            type="text"
            name="author"
            placeholder="Adicione o autor"
        />
        </div>
        <div class="form-control">
        <label>ISBN#</label>
        <input 
            type="text" 
            name="isbn" 
            placeholder="Adicione o ISBN" 
        />
        </div>
        <div class="form-control form-control-check">
        <input 
            type="checkbox" 
            name="readIt" 
            id="readIt" 
            />
        <label for="readIt">Já li o livro</label>
        </div>
 
        <button type="submit" class="btn btn-block" @click="addNewBook()">Salvar livro</button>
    </form>

</template>

<style>

</style>