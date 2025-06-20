<template>
    <main>
        <p>{{ labelVisual }}</p>
        <h1>{{ amountCurrency }}</h1>
        <div class="graphic">
          <slot name="graphic"></slot>
        </div>
        <div class="action">
          <slot name="action"></slot>
        </div>
    </main>
</template>
<script setup>
    import {computed} from 'vue'
    const currencyFormatter = new Intl.NumberFormat("es-CO", {
      style:"currency",
      currency:"COP"
    })
    const {totalLabel,label, totalAmount, amount} = defineProps({
            totalLabel:String,      
            label: String,
            totalAmount: Number,
            amount: Number
            })
    const labelVisual = computed(()=>{
      console.log('label:',label)
      console.log('amount:',label)
        return label !== null ? label : totalLabel
    })        
    const amountVisual = computed(()=>{
        return amount !== null ? amount : totalAmount
    })
    const amountCurrency = computed(()=>{
      return currencyFormatter.format(amountVisual.value)
    })
</script>
<style scoped>
main {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  width: 100%;
}

h1,
p {
  margin: 0;
  text-align: center;
}

h1 {
  margin-top: 14px;
  color: var(--brand-green);
}

.graphic {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  padding: 48px 24px;
  box-sizing: border-box;
}
</style>