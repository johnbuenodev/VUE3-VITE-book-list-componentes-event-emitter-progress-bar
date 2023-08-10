<script setup>

import {ref, reactive} from 'vue';

const emit = defineEmits(['closeAddBook','addNewBook']);

const props = defineProps(['newId']);

function closeAddBook() {
  emit('closeAddBook');
}

function addNewBook() {
    console.log(newBook);
    if(newBook.title !== "" && newBook.author !== "") {

        console.log(newBook);
        emit('addNewBook', newBook);

    }

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
            required
            type="text"
            name="text"
            placeholder="Adicione o título"
            v-model="newBook.title"
        />
        </div>
        <div class="form-control">
        <label>Capa</label>
        <input 
            type="text" 
            name="cover" 
            placeholder="Adicione o link da imagem de capa"
            v-model="newBook.cover"
            />
        </div>
        <div class="form-control">
        <label>Autor</label>
        <input
            required
            type="text"
            name="author"
            placeholder="Adicione o autor"
            v-model="newBook.author"
        />
        </div>
        <div class="form-control">
        <label>ISBN#</label>
        <input 
            type="text" 
            name="isbn" 
            placeholder="Adicione o ISBN" 
            v-model="newBook.isbn"
        />
        </div>
        <div class="form-control form-control-check">
        <input 
            type="checkbox" 
            name="readIt" 
            id="readIt" 
            v-model="newBook.isRead"
            />
        <label for="readIt">Já li o livro</label>
        </div>
 
        <!-- preventDefault quando aplica o submit para não recarregar a pagina -->
        <button  class="btn btn-block" type="submit" @click.prevent="addNewBook()">Salvar livro</button>
    </form>

</template>

<style>

</style>