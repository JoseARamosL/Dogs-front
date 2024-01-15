<template>
  <div>
    <q-table
        :rows="dogs"
        :columns="columns"
        row-key="id"
    />
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
          } else {
            console.error('La respuesta de la API no es un array:', response.data);
          }
        })
        .catch(error => {
          console.error('Error al obtener la lista de perros:', error);
        });
  },
};
</script>
