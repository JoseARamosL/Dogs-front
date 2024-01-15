<template>
  <div>
    <q-table
        :rows="dogs"
        :columns="columns"
        row-key="id"
        @row-click="showDogFormEdit"
    />

    <q-dialog
      v-model="showForm.show"
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
          <q-btn v-if="showForm.update" label="Editar" color="primary" />
          <q-btn v-if="showForm.create" label="Crear" color="primary" @click="addNewDog"/>
          <q-btn label="Cerrar" color="red" @click="closeForm" />
        </q-card-actions>
      </q-card>
    </q-dialog>

    <q-btn label="Añadir perro" color="primary" @click="showDogFormCreate" class="q-mt-md" />
  </div>
</template>

<script>
export default {
  data() {
    return {
      dogs: [],
      columns: [
        { name: 'image', label: 'Imagen', align: 'center', field: 'img_uri',
        format: (value, row) => {
          return value ? `<img src="${value}" alt="Dog Image" style="max-width: 50px; max-height: 50px;" />` : 'Imagen no disponible';
        },
        },
        { name: 'name', label: 'Nombre', align: 'left', field: 'name' },
        { name: 'description', label: 'Descripción', align: 'left', field: 'description' },
        { name: 'race_id', label: 'Raza ID', align: 'center', field: 'race_id' },
        { name: 'size_ide', label: 'Tamaño ID', align: 'center', field: 'size_id'}
      ],
      showForm: {
        show: false,
        create: false,
        update: false
      },
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
    showDogFormEdit(event, selectedRow) {
      this.selectedDog = { ...selectedRow };
      this.showForm.show = true;
      this.showForm.update = true;
      this.showForm.create = false;
    },
    closeForm() {
      this.showForm.show = false;
      this.showForm.update = false;
      this.showForm.create = false;
      this.clearSelectedDog();
    },
    clearSelectedDog() {
      this.selectedDog = {
        name: '',
        description: '',
        race_id: '',
        size_id: '',
        hair_id: 1,
        country_id: 1
      };
    },
    showDogFormCreate() {
      this.showForm.show = true;
      this.showForm.update = false;
      this.showForm.create = true;
    },
    async addNewDog() {
      try {
        const response = await this.$axios.post('/dog/create', this.selectedDog);

        if (response.status === 201) {
          console.log('Perro creado con éxito:', response.data.data);
          this.dogs.push(response.data.data);
          this.closeForm();
        } else {
          console.error('Error al crear el perro:', response.data.message);
        }
      } catch (error) {
        console.error('Error al crear el perro:', error);
      }
    }
  }
};
</script>
