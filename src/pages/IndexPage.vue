<template>
  <q-page>
  <div class="q-pa-md">
    <q-table
      title="Treats"
      :rows="row"
      :columns="columns"
      row-key="name"
      :filter="filter"
      :loading="loading"
    >
    <template v-slot:top>
      <q-space />
      <div class="row item-centre q-gutter-sm">
          <q-btn color="grey" @click="showFilter = true" label="filter" />
          <q-input outlined debounce="200" color="primary" v-model="filter" placeholder="search..." class="rounded-input">
          <template v-slot:append>
          <q-icon name="search" />
          </template>
        </q-input>
      </div>
    </template>
  </q-table>

   <q-dialog v-model="showFilter">
      <q-card>
        <q-card-section>
          <div class="text-h6">filter</div>
        </q-card-section>

        <q-card-section class="q-pt-none">
          <q-select outlined v-model="model" :options="options" label="Outlined" />
        </q-card-section>

        <q-card-actions align="right">
          <q-btn flat label="OK" color="primary" v-close-popup />
        </q-card-actions>
      </q-card>
    </q-dialog>


  </div>
  </q-page>
</template>

<script>
import { ref } from 'vue'
const columns = [
  {
    name: 'name',
    required: true,
    label: 'name',
    align: 'left',
    field: row => row.name,
    format: val => `${val}`,
    sortable: true
  },
  { name: 'calories', align: 'center', label: 'Calories', field: 'calories', sortable: true },
  { name: 'fat', label: 'Fat (g)', field: 'fat', sortable: true },
  { name: 'carbs', label: 'Carbs (g)', field: 'carbs' },
  { name: 'protein', label: 'Protein (g)', field: 'protein' },
  { name: 'sodium', label: 'Sodium (mg)', field: 'sodium' },
  { name: 'calcium', label: 'Calcium (%)', field: 'calcium', sortable: true, sort: (a, b) => parseInt(a, 10) - parseInt(b, 10) },
  { name: 'iron', label: 'Iron (%)', field: 'iron', sortable: true, sort: (a, b) => parseInt(a, 10) - parseInt(b, 10) }
]

const rows = [
  {
    name: 'Frozen Yogurt',
    calories: 159,
    fat: 6.0,
    carbs: 24,
    protein: 4.0,
    sodium: 87,
    calcium: '14%',
    iron: '1%'
  },
  {
    name: 'Ice cream sandwich',
    calories: 237,
    fat: 9.0,
    carbs: 37,
    protein: 4.3,
    sodium: 129,
    calcium: '8%',
    iron: '1%'
  },
  {
    name: 'Eclair',
    calories: 262,
    fat: 16.0,
    carbs: 23,
    protein: 6.0,
    sodium: 337,
    calcium: '6%',
    iron: '8%'
  }
]

export default {
  setup () {
    const model = ref(null)
    const options = ['calories<200','calories>200']
    const showFilter = ref(false)
    const filter = ref('')
    const row = ref(rows)
    return {
      columns,
      row,
      filter,
      showFilter,
      model,
      options
    }
  }
}
</script>
