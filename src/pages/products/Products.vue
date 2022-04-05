<template>
  <div class="q-pa-md">
    <q-table title="Treats" :rows="products" :columns="columns" row-key="name">
      <template v-slot:body-cell-img="props">
        <q-td key="bookmark" :props="props">
          <q-img
            :src="props.row.image"
            loading="lazy"
            spinner-color="white"
            height="140px"
            style="max-width: 80px"
          />
        </q-td>
      </template>
      <template v-slot:body-cell-actions="props">
        <q-td key="bookmark" :props="props">
          <q-btn
            color="red"
            text-color="black"
            label="Delete"
            @click="del(props.row.id)"
          />
        </q-td>
      </template>
    </q-table>
  </div>
</template>

<script lang="ts">
import { api } from 'src/boot/axios';
import { defineComponent } from 'vue';

const columns = [
  {
    name: 'id',
    label: '#',
    align: 'left',
    field: 'id',
  },
  {
    name: 'image',
    label: 'Image',
    align: 'left',
    field: 'image',
  },
  {
    name: 'title',
    label: 'Title',
    align: 'left',
    field: 'title',
  },
  {
    name: 'description',
    label: 'Description',
    align: 'left',
    field: 'description',
  },
  {
    name: 'price',
    label: 'Price',
    align: 'left',
    field: 'price',
  },
  {
    name: 'actions',
    label: 'Actions',
    align: 'left',
    field: '',
  },
];

export default defineComponent({
  name: 'ProductsPage',
  data() {
    return {
      products: [],
      columns,
    };
  },
  async mounted() {
    this.fetchProducts();
  },
  methods: {
    async fetchProducts() {
      const { data } = await api.get('products');
      this.products = data;
    },
    async del(id: number) {
      if (confirm('Are you sure?')) {
        await api.delete(`products/${id}`);
        this.fetchProducts();
      }
    },
  },
});
</script>
