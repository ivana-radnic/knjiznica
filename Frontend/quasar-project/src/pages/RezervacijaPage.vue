<template>
    <q-page padding>
      <div class="q-pa-md">
        <q-table
          separator="horizontal"
          title="Rezervacija"
          title-class="text-h4 text-bold text-red-9"
          :rows="books"
          :columns="columns"
          row-key="id"
          table-class="text-black"
          table-style="border: 3px solid black;"
          table-header-style="height: 65px"
          table-header-class="bg-red-2"
          bordered
          flat
          square
        >
          <template v-slot:header="props">
            <q-tr :props="props">
              <q-th
              v-for="col in props.cols"
              :key="col.name"
              :props="props"
              >
                {{ col.label }}
              </q-th>
            </q-tr>
          </template>
          <template v-slot:body="props">
            <q-tr :props="props">
              <q-td v-for="col in props.cols"
                :key="col.name"
                :props="props">
                <span v-if="col.name !='slika' && col.name!='opis'" >
                  {{ col.value }}
                </span>
                <div v-if="col.name=='opis'">
                  <div class="tbl_opis">
                    {{ props.row.opis }}
                  </div>
                </div>
                <q-img
                  :src="props.row.slika"
                  v-if="col.name =='slika'"
                  size="100px" class="shadow-10">
                </q-img>
              </q-td>
            </q-tr>
          </template>
        </q-table>
  
      </div>
    </q-page>
  
  </template>
  <script>
  import { ref } from 'vue'
  import axios from 'axios';
  
  const style1 = {
        fontSize:'18px'
      };
  const style2 = {
        fontSize: '24px'
      };
  
  const columns = [
    {
      name:'id',
      label:'id',
      field:'id',
      align:'left',
      sortable: true,
      style: style1,
      headerStyle: style2
    },
    {
      name: 'naslov',
      label: 'naslov',
      field: 'naslov',
      align:'left',
      sortable: true,
      style: style1,
      headerStyle: style2
    },
    {
      name: 'autor',
      label: 'autor',
      field: 'autor',
      align: 'left',
      style: style1,
      headerStyle: style2
    },
    {
      name: 'opis',
      label: 'opis',
      field: 'opis',
      align: 'left',
      style: style1,
      headerStyle: style2
    },
    {
      name: 'slika',
      label: 'slika',
      field: 'slika',
      align:'center',
      style: style1,
      headerStyle: style2
    },
    {
      name: 'stanje',
      label: 'stanje',
      field: 'stanje',
      align:'center',
      style: style1,
      headerStyle: style2
    },
    {
      name: 'korisnik',
      label: 'korisnik',
      field: 'korisnik',
      align:'center',
      style: style1,
      headerStyle: style2
    },
    {
      name: 'datum_rezervacije',
      label: 'datum_rezervacije',
      field: 'datum_rez',
      align:'center',
      style: style1,
      headerStyle: style2
    }
  ];
  let books = ref([])
  
  export default {
    setup () {
      return {
        columns,
        books,
        pagination: ref({
          rowsPerPage: 10
        }),
      }
    },
  
    mounted() {
      this.loadBooks()
    },
    methods: {
      async loadBooks() {
        await axios.get('http://localhost:3000/api/rezerv_knjige')
          .then(result => {
            console.log(result.data)
            this.books = result.data
            console.log(this.books[0].id)
          })
          .catch(error => {
            console.error(error)
          })
      },
    }
  }
  </script>