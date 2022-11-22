<template>
    <div
      class="list_block"
      ref="item"
      :class="{left: align === 'left' ,center: align === 'center' , right: align === 'right' }"
    >
      <div class="items"
           v-for="(item , i  ) in array"
           :key="i"
           id="items"
           ref="items"
      >
        <v-icon class="lll" v-if="item.separator">{{ icon ??  'mdi-circle-small' }}</v-icon>
          {{item.text}}
      </div>
    </div>
</template>

<script>
  export default {
    name: 'AppListOverflowed',
    props:{
      items:{
        type:Array,
        required: true
      },
      icon:String,
      align:String
    },
    data: function () {
      return {
        array: this.items,
      }
    },
    async mounted() {
      if(!this.array) return  alert('missing prop') //miss props

      this.array = this.add_separator(this.array) //Добавление элементов разделителей в массив
      this.$nextTick(() => { //заюзал по той причине,что не успевал получить правильное свойтсво ширины,страница не до конца была отрендерена
        let length = this.max_length(this.$refs.items , this.$refs.item.offsetWidth) // вычисление максимального колличества элементов которые помещаются
        this.array.splice(length) // удаление не нужных частей
        if(this.array[length-1].separator) this.array.pop(length-1) //доудаление есть вдруг остался сепаратор
      })

    },
    methods:{
      add_separator(array){ //Добавление разделителей в массив
        let arr = []
        array.map((el , index) => {
          if(array.length >= index+1){
            if(index != 0 )arr.push({separator:true})
            arr.push(el)
          }
        })
        return arr
      },
      max_length(array , max_width){ // вычисление максимального кол-ва элементов которые помещаются в контейнер
        let length = 0
        let array_child = array
        let width_elements = 0
        for (let i = 0; i < array_child.length; i++) {
          if (max_width > width_elements) {
            length += 1
            width_elements += array_child[i].clientWidth
          }
        }
        return length -2
      },

    },

  }
</script>

<style scoped lang="scss">
.list_block{
  background: #e30404;
  display: flex;
}
.left{
  justify-content: flex-start;
}
.right{
  justify-content: flex-end;
}
.center{
  justify-content: space-between;
}
.items{
  position: relative;
  word-break: initial;
  white-space: nowrap;
}
</style>
