<template>
  <div>
    <q-table
      :rows="dogs"
      :columns="columns"
      row-key="id"
      @row-click="showDogFormEdit"
    >

      <template v-slot:body-cell-race="{ row }">
        <q-td>
          <div class="text-center" v-if="row['race'] && row['race']['race']">{{ row['race']['race'] }}</div>
          <div v-else>Nombre de raza no disponible</div>
        </q-td>
      </template>

      <template v-slot:body-cell-size="{ row }">
        <q-td>
          <div class="text-center" v-if="row['size'] && row['size']['size']">{{ row['size']['size'] }}</div>
          <div v-else>Tamaño no disponible</div>
        </q-td>
      </template>

      <template v-slot:body-cell-hair="{ row }">
        <q-td>
          <div class="text-center" v-if="row['hair'] && row['hair']['hair']">{{ row['hair']['hair'] }}</div>
          <div v-else>Pelo no disponible</div>
        </q-td>
      </template>

      <template v-slot:body-cell-delete="{ row }">
        <q-td>
          <div class="q-gutter-md text-center">
            <q-btn
              icon="delete"
              color="negative"
              @click.stop="deleteDog(row)"
            />
          </div>
        </q-td>
      </template>

    </q-table>

    <q-dialog
      v-model="showForm.show"
      persistent
      @hide="clearSelectedDog">
      <q-card>
        <q-card-section>
          <q-input v-model="selectedDog.name" label="Nombre" />
          <q-input v-model="selectedDog.description" label="Descripción" />
          <q-select
            v-model="selectedDog.race_id"
            :options="races.map(race => ({label: race.race, value: race.id}))"
            label="Raza"/>
          <q-select
            v-model="selectedDog.size_id"
            :options="sizes.map(size => ({label: size.size, value: size.id}))"
            label="Tamaño"/>
          <q-select
            v-model="selectedDog.hair_id"
            :options="hairs.map(hair => ({label: hair.hair, value: hair.id}))"
            label="Pelo"/>
        </q-card-section>



        <q-card-actions align="right">
          <q-btn v-if="showForm.update" label="Editar" color="primary" @click="updateDog"/>
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
      races: [],
      sizes: [],
      hairs: [],
      columns: [
        { name: 'name', label: 'Nombre', align: 'left', field: 'name' },
        { name: 'description', label: 'Descripción', align: 'left', field: 'description' },
        { name: 'race', label: 'Raza', align: 'center', field: 'race_id' },
        { name: 'size', label: 'Tamaño', align: 'center', field: 'size_id'},
        { name: 'hair', label: 'Pelo', align: 'center', field: 'hair_id'},
        { name: 'delete', label: 'Eliminar', align: 'center', field: 'id' }
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
        size_id: '',
        img_uri: ''
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
    async showDogFormEdit(event, selectedRow) {
      try {
        const responseR = await this.$axios.get('/races');
        if (Array.isArray(responseR.data.data)) {
          this.races = responseR.data.data;
        }

        const responseS = await this.$axios.get('/sizes');
        if (Array.isArray(responseS.data.data)) {
          this.sizes = responseS.data.data;
        }

        const responseH = await this.$axios.get('/hairs');
        if (Array.isArray(responseH.data.data)) {
          this.hairs = responseH.data.data;
        }
      } catch (error) {
        console.error('Error al obtener la lista de razas:', error);
      }
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
        hair_id: '',
        country_id: 1
      };
    },
    async showDogFormCreate() {
      try {
        const responseR = await this.$axios.get('/races');
        if (Array.isArray(responseR.data.data)) {
          this.races = responseR.data.data;
        }

        const responseS = await this.$axios.get('/sizes');
        if (Array.isArray(responseS.data.data)) {
          this.sizes = responseS.data.data;
        }

        const responseH = await this.$axios.get('/hairs');
        if (Array.isArray(responseH.data.data)) {
          this.hairs = responseH.data.data;
        }
      } catch (error) {
        console.error('Error al obtener la lista de razas:', error);
      }
      this.showForm.show = true;
      this.showForm.update = false;
      this.showForm.create = true;
    },
    async addNewDog() {
      try {
        const data = {
          name: this.selectedDog.name,
          description: this.selectedDog.description,
          race_id: this.selectedDog.race_id.value,
          hair_id: this.selectedDog.hair_id.value,
          size_id: this.selectedDog.size_id.value,
          country_id: this.selectedDog.country_id
        };
        const response = await this.$axios.post('/dog/create', data);

        if (response.status === 201) {
          console.log('Perro creado con éxito:', response.data.data);
          this.dogs.push(response.data.data);
          this.closeForm();
          window.location.reload();
        } else {
          console.error('Error al crear el perro:', response.data.message);
        }
      } catch (error) {
        console.error('Error al crear el perro:', error);
      }
    },
    async deleteDog(row) {
      try {
        const dogId = row.id;
        const response = await this.$axios.delete(`/dog/${dogId}`);

        if (response.status === 204) {
          const index = this.dogs.findIndex(dog => dog.id === dogId);
          if (index !== -1) {
            this.dogs.splice(index, 1);
          }
        } else {
          console.error('Error al eliminar el perro:', response.data.message);
        }
      } catch (error) {
        console.error('Error al eliminar el perro:', error);
      }
    },
    async updateDog() {
      try {
        const race_id = typeof this.selectedDog.race_id === 'object' ?
          this.selectedDog.race_id.value : this.selectedDog.race_id;

        const size_id = typeof this.selectedDog.size_id === 'object' ?
          this.selectedDog.size_id.value : this.selectedDog.size_id;

        const hair_id = typeof this.selectedDog.hair_id === 'object' ?
          this.selectedDog.hair_id.value : this.selectedDog.hair_id;

        const data = {
          name: this.selectedDog.name,
          description: this.selectedDog.description,
          race_id: race_id,
          hair_id: hair_id,
          size_id: size_id,
          country_id: this.selectedDog.country_id
        };
        console.log(this.selectedDog);
        console.log(data);
        const response = await this.$axios.put(`/dog/${this.selectedDog.id}`, data);


        if (response.status === 200) {
          const index = this.dogs.findIndex(dog => dog.id === this.selectedDog.id);
          if (index !== -1) {
            this.dogs.splice(index, 1, response.data.data);
          }

          this.closeForm();
          window.location.reload();
        } else {
          console.error('Error al editar el perro:', response.data.message);
        }
      } catch (error) {
        console.error('Error al editar el perro:', error);
      }
    }
  }
};
</script>

