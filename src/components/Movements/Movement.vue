<template>
    <div class="movement">
        <div class="content">
            <h4>{{title}}</h4>
            <p>{{description}}</p>
        </div>
        <div class="action">
            <img src="@/assets/trash-icon.svg" alt="borrar" @click="remove"/>
            <p :class="{'red' : isNegative, 'green' : !isNegative}">{{ amountCurrency }}</p>
        </div>
    </div>
</template>

<script setup>
import {computed} from "vue"
const currencyFormatter = new Intl.NumberFormat("es-CO", {
      style:"currency",
      currency:"COP"
    })
    const props = defineProps({
        id: Number,
        title: String,
        description: String,
        amount: Number
    })

    const amountCurrency = computed(()=>{
        return currencyFormatter.format(props.amount)
    })

    const isNegative = computed(()=>{
        return props.amount < 0
    })

    const emit = defineEmits(["remove"])

    function remove(){
        emit("remove", props.id)
    }


    
</script>

<style scoped>
.movement {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  padding: 16px;
  background-color: #e6f9ff;
  border-radius: 8px;
  box-sizing: border-box;
}

.movement .content {
  width: 100%;
}

.movement .action {
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  flex-direction: column;
}

h4,
p {
  margin: 0;
  padding: 0;
}

h4 {
  margin-bottom: 8px;
}

.movement .action img {
  margin-bottom: 16px;
}

.red {
  color: red;
}

.green {
  color: green;
}
</style>