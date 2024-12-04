<template>
  <q-page padding>
    <div class="q-pa-md">
      <q-input
        v-model="searchQuery"
        label="Unesite naziv ili autora knjige"
        outlined
        clearable
      />

      <div class="q-my-md">
        <q-checkbox v-model="searchByTitle" label="Pretraži po naslovu" />
        <q-checkbox v-model="searchByAuthor" label="Pretraži po autoru" />
      </div>

      <q-btn label="Traži" color="primary" @click="performSearch" />

      <q-table
        v-if="filteredBooks.length"
        :rows="filteredBooks"
        :columns="columns"
        row-key="id"
        title="Rezultati Pretraživanja"
        class="q-mt-md"
      />
    </div>
  </q-page>
</template>


<script>
import { ref } from 'vue';

export default {
  setup() {
    const searchQuery = ref('');
    const searchByTitle = ref(true);
    const searchByAuthor = ref(false);

    const columns = [
      { name: 'id', label: 'ID', align: 'left', field: row => row.id },
      { name: 'naslov', label: 'Naslov', align: 'left', field: row => row.naslov },
      { name: 'autor', label: 'Autor', align: 'left', field: row => row.autor },
      { name: 'opis', label: 'Opis', align: 'left', field: row => row.opis },
      { name: 'stanje', label: 'Stanje', align: 'right', field: row => row.stanje }
    ];

    const books = [
        { id: 1, naslov: 'Razmišljaj brzo i sporo', autor: 'Daniel Kahneman', opis: 'Proučavanje psiholoških mehanizama donošenja odluka i utjecaja brzih i sporih sustava mišljenja.', stanje: 3 },
        { id: 2, naslov: '1984', autor: 'George Orwell', opis: 'Distopijski roman o totalitarizmu, propagandi i nadzoru.', stanje: 11 },
        { id: 3, naslov: 'Bogati otac, siromašni otac', autor: 'Robert T. Kiyosaki', opis: 'Financijski vodič koji istražuje razliku između pristupa bogatih i siromašnih prema novcu.', stanje: 23 },
        { id: 4, naslov: 'Lovac u žitu', autor: 'J.D Salinger', opis: 'Kultni roman o mladenačkoj pobuni i otuđenju.', stanje: 10 },
        { id: 5, naslov: 'Harry Potter i Kamen mudraca', autor: 'J.K Rowling', opis: 'Prva knjiga u serijalu o mladom čarobnjaku Harryju Potteru i njegovim pustolovinama u Hogwartsu.', stanje: 51 }
      ]
const filteredBooks = ref([]);

const performSearch = () => {
  if (!searchQuery.value) {
    filteredBooks.value = [];
    return;
  }
  filteredBooks.value = books.filter(book => {
    const matchesTitle = searchByTitle.value && book.naslov.toLowerCase().includes(searchQuery.value.toLowerCase());
    const matchesAuthor = searchByAuthor.value && book.autor.toLowerCase().includes(searchQuery.value.toLowerCase());
    return matchesTitle || matchesAuthor;
  });
};

return {
  searchQuery,
  searchByTitle,
  searchByAuthor,
  columns,
  books,
  filteredBooks,
  performSearch
};
}
};
</script>