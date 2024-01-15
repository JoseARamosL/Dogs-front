<template>
  <div>
    <q-table
        :rows="dogs"
        :columns="columns"
        row-key="id"
        @row-click="showDogForm"
    />

    <q-dialog
      v-model="showForm"
      persistent
      @hide="clearSelectedDog">
      <q-card>
        <q-card-section>
          <q-input v-model="selectedDog.name" label="Nombre" />
          <q-input v-model="selectedDog.description" label="Descripción" />
          <q-input v-model="selectedDog.race_id" label="Raza ID" />
          <q-input v-model="selectedDog.size_id" label="Tamaño ID" />
        </q-card-section>

        <q-card-actions align="right">
          <q-btn label="Cerrar" color="primary" @click="closeForm" />
        </q-card-actions>
      </q-card>
    </q-dialog>
  </div>
</template>

<script>
export default {
  data() {
    return {
      dogs: [],
      columns: [
        { name: 'name', label: 'Nombre', align: 'left', field: 'name' },
        { name: 'description', label: 'Descripción', align: 'left', field: 'description' },
        { name: 'race_id', label: 'Raza ID', align: 'center', field: 'race_id' },
        { name: 'size_ide', label: 'Tamaño ID', align: 'center', field: 'size_id'}
      ],
      showForm: false,
      selectedDog: {
        name: '',
        description: '',
        race_id: '',
        size_id: ''
      }
    };
  },
  mounted() {
    this.$axios.get('/dogs')
        .then(response => {
          if (Array.isArray(response.data.data)) {
            this.dogs = response.data.data.map(dog => {
              const { created_at, updated_at, ...dogData } = dog;
              return dogData;
            });

            console.log(this.dogs);
          } else {
            console.error('La respuesta de la API no es un array:', response.data);
          }
        })
        .catch(error => {
          console.error('Error al obtener la lista de perros:', error);
        });
  },
  methods: {
    showDogForm(event, selectedRow) {
      this.selectedDog = { ...selectedRow };
      this.showForm = true;
    },
    closeForm() {
      this.showForm = false;
    },
    clearSelectedDog() {
      this.selectedDog = {
        name: '',
        description: '',
        race_id: '',
        size_id: ''
      };
    }
  }
};
</script>
