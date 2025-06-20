<template>
    <Layout>
        <template #header>
            <Header></Header>
        </template>
        <template #resume>
            <Resume
                :total-label="'Ahorro Total'"
                :label="label"
                :total-amount="totalAmount"
                :amount="amount"
            >
            <template #graphic>
                <Graphic :amounts="amounts" @select="select"/>
            </template>
            <template #action>
                <Action @create="create"/>
            </template>
            </Resume>
        </template>
        <template #movements>
            <Movements
                :movements="movements"
                @remove="remove"
            />
        </template>
    </Layout>
</template>

<script setup>
    import Layout from "./Layout.vue"
    import Header from "./Header.vue"
    import Resume from "./Resume/Index.vue"
    import Graphic from "./Resume/Graphic.vue"
    import Action from "./Action.vue"
    import Movements from "./Movements/Index.vue"
    import {ref, computed, onMounted} from "vue"

    const label = ref(null)
    const amount = ref(null)
    const movements = ref([])

    const amounts = computed(()=>{
        const lastDays = movements.value.filter(m => {
            const today = new Date()
            console.log('today',today)
            const oldDate = new Date(today)
            oldDate.setDate(today.getDate() - 30)
            console.log('oldDate',oldDate)
            console.log('m:', m.time)
            return m.time >= oldDate
        }).map(m => m.amount)

        return lastDays.map((m,i) =>{
            const lastMovements = lastDays.slice(0,i)
            return lastMovements.reduce((suma, movement)=>{
                return suma + movement
            },0)
        })
    })
    console.log('amounts:', amounts.value)

    function create(movement){
        movements.value.push(movement)
        save()
    }
    function remove(id){
        const index = movements.value.findIndex(m=>m.id === id)
        movements.value.splice(index, 1)
    }

    function save(){
        localStorage.setItem("movements", JSON.stringify(movements.value))
    }

    // function select(el) {
    //   console.log(el);
    //   amount.value = el;
    // }

    const totalAmount = computed(()=>{
        return movements.value.reduce((suma, m) =>{
            return suma + m.amount
        },0)
    })

    onMounted(()=>{
        const movementsList = JSON.parse(localStorage.getItem("movements"))
        console.log('movementsList:', movementsList)
        if(Array.isArray(movementsList)){
        movements.value = movementsList.map(m=>{
            return{...m, time: new Date(m.time)}
            
        })
    }
    })


</script>