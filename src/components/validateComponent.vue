<template>
  <div class="validate-wrap">
    On {{ this.id }} comp {{ text }}
    <button @click="validateComp($props.id)">Вызвать метод</button>
    <slot name="some"></slot>
    <slot :validate="validate" name="valComp"></slot>
  </div>
</template>

<script>
export default {
  name: "validateComponent",
  props: {
    id: Number,
    validate: Function
  },
  data: () => ({
    text: `False`
  }),
  methods: {
    validateComp(id) {
     // Решил реализовать с помощью slot и вызывать дочерние методы так же через $slots
     // Здесь мы заходим в наши слоты и вызываем только с именем valComp, в случае если слот лежит в неком компоненте - то заходим в слоты этого компонента и ищем уже там 
      if (this.id === id) {
        console.log(this.$slots)
        for (let item in this.$slots) {
          if (item === 'valComp') {
            this.$slots[item][0].componentInstance.validateComp(id);
          }
          if (item === 'some') {
            for (let someItem in this.$slots[item]) {
              for (let slotItem in this.$slots[item][someItem].componentInstance.$slots) {
                if (slotItem === 'valComp') {
                  for (let someSlotItem in this.$slots[item][someItem].componentInstance.$slots[slotItem]) {
                    this.$slots[item][someItem].componentInstance.$slots[slotItem][someSlotItem].componentInstance.validateComp(id);
                  }
                }
              }
            }
          }
        }
      }
      this.text = 'True';
    }
  },
  mounted () {
  }
}

</script>

<style scoped>

</style>