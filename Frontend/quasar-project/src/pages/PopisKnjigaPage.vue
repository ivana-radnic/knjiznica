<template>
  <q-page padding>
    <!-- Naslov i popratni tekst -->
    <div class="text-center q-mb-md">
      <h1>Popis knjiga</h1>
      <p>Pregled svih dostupnih knjiga u knjižnici.</p>
    </div>

    <!-- Tablica s podacima knjiga -->
    <q-table
      :rows="books"
      :columns="columns"
      row-key="id"
      :filter="filter"
    >
    </q-table>
  </q-page>
</template>

<script>
export default {
  setup() {
    // Podaci o knjigama (bez slika)
    const books = [
      {
        id: 1,
        naslov: 'Razmišljaj brzo i sporo',
        autor: 'Daniel Kahneman',
        opis: 'Proučavanje psiholoških mehanizama donošenja odluka i utjecaja brzih i sporih sustava mišljenja.',
        slika: '', // Ovdje možete staviti praznu putanju ili ukloniti ovo polje
        stanje: 3
      },
      {
        id: 2,
        naslov: '1984',
        autor: 'George Orwell',
        opis: 'Distopijski roman o totalitarizmu, propagandi i nadzoru',
        slika: '', // Ovdje možete staviti praznu putanju ili ukloniti ovo polje
        stanje: 11
      },
      {
        id: 3,
        naslov: 'Bogati otac, siromašni otac',
        autor: 'Robert T. Kiyosaki',
        opis: 'Financijski vodič koji istražuje razliku između pristupa bogatih i siromašnih prema novcu.',
        slika: '', // Ovdje možete staviti praznu putanju ili ukloniti ovo polje
        stanje: 23
      },
{
        id: 4,
        naslov: 'Lovac u žitu',
        autor: 'J.D Salinger',
        opis: 'Kultni roman o mladenačkoj pobuni i otuđenju.',
        slika: '', // Ovdje možete staviti praznu putanju ili ukloniti ovo polje
        stanje: 10
      },
      {
        id: 5,
        naslov: 'Harry Potter i Kamen mudraca',
        autor: 'J.K Rowling',
        opis: 'Prva knjiga u serijalu o mladom čarobnjaku Harryju Potteru i njegovim pustolovinama u Hogwartsu.',
        slika: '', // Ovdje možete staviti praznu putanju ili ukloniti ovo polje
        stanje: 51
      }
    ];

    // Kolone za tablicu
    const columns = [
      { name: 'id', label: 'ID', align: 'left', field: 'id' },
      { name: 'naslov', label: 'Naslov', align: 'left', field: 'naslov' },
      { name: 'autor', label: 'Autor', align: 'left', field: 'autor' },
      { name: 'opis', label: 'Opis', align: 'left', field: 'opis' },
      { name: 'slika', label: 'Slika', align: 'center', field: 'slika', format: val => '' }, // Bez prikaza slike
      { name: 'stanje', label: 'Stanje', align: 'center', field: 'stanje' }
    ];

    // Filtriranje (opcionalno)
    const filter = '';

    return {
      books,
      columns,
      filter
    };
  }
};
</script>

<style scoped>
.q-page {
  padding: 20px;
}

.text-center {
  text-align: center;
}

.q-mb-md {
  margin-bottom: 20px;
}
.q-table {
  margin-top: 20px;
}
</style>