<template>
    <Layout>
        <template #header>
            <Header></Header>
        </template>
        <template #resume>
            <Resume
                :total-label="'Ahorro Total'"
                :label="label"
                :total-amount="1000000"
                :amount="10000"
            >
            <template #graphic>
                graphic
            </template>
            <template #action>
                action
            </template>
            </Resume>
        </template>
        <template #movements>
            <Movements
                :movements="movements"
            />
        </template>
    </Layout>
</template>

<script setup>
    import Layout from "./Layout.vue"
    import Header from "./Header.vue"
    import Resume from "./Resume/Index.vue"
    import Movements from "./Movements/Index.vue"
    import {ref} from "vue"

    const movements = ref([
  {
    id: 0,
    title: "Movimiento 1",
    descripcion: "Nuevo movimiento",
    amount: 1000
  },

  {
    id: 1,
    title: "Movimiento 2",
    descripcion: "Nuevo movimiento",
    amount: 1000
  }
])


</script>