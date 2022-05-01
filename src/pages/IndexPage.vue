<template>
  <q-page class="">
      <div class="q-pa-md">
        <q-table
          grid
          :rows="coins"
          :columns="columns"
          row-key="id"
          :filter="filter"
          hide-header
          :pagination="{rowsPerPage: 15}"
          :rows-per-page-options="[12,15,20]"
        >
          <template v-slot:item="props">
            <div class="q-pa-xs col-xs-12 col-sm-6 col-md-4">
              <q-card>
                <q-card-section class="text-center">
                  <span class="text-h6">
                    {{ props.row.name }}
                  </span>
                </q-card-section>
                <q-separator></q-separator>
                <q-card-section class="flex flex-center text-center" style="font-size:20px">
                  {{ props.row.symbol }}
                </q-card-section>
                <q-card-section class="flex flex-center">
                  <q-btn
                    size="lg"
                    color="primary"
                    label="View"
                    @click="navToCryptoDetails(props.row.id)"
                  ></q-btn>
                </q-card-section>
              </q-card>
            </div>
          </template>
          <template v-slot:top-right>
            <q-input borderless dense debounce="300" v-model="filter" placeholder="Search">
              <template v-slot:append>
                <q-icon name="search" />
              </template>
            </q-input>
          </template>
        </q-table>
      </div>
  </q-page>
</template>

<script>
import { ref } from 'vue'
import { useRouter } from 'vue-router'
export default {
  async created(){
    try{
      const res = await this.$api.get("coins/list");
      res.status === 200 
        ? this.coins = res.data
        : alert('Some error occured1.')
    }catch(error){
      alert('Some error occured2.')
    }
  },
  setup() {
    const router = useRouter()
    const coins = ref([]);
    const columns = ref([
      { name: 'name', align: 'center',label: 'Name', field: 'name' },
      { name: 'symbol', align: 'center', label: 'Symbol', field: 'symbol'}
    ])
    const filter = ref("")
    function navToCryptoDetails(id) {
      router.push({ name: 'CryptoDetails', params: {id}})
    }
    return {
      coins,
      columns,
      filter,
      navToCryptoDetails
    }
  }
}
</script>
