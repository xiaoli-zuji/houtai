<template>
  <div>
    子组件1
    <br /><br />
    <ul>
      <li v-for="item in list" :key="item.id">
        {{ item.name }} --- {{ item.address }}
      </li>
    </ul>
    <br /><br />
    <button @click="sendValueToParent">传值给父组件</button>
    <br /><br />
     <button @click="sendValueToChild2">传值给Child2</button>
  </div>
</template>

<script>
import bus from './bus'
export default {
  name: "Child1",
  // props: ['list']
  // props: {
  //     list: Array
  // }
  props: {
    list: {
      type: Array,
      // required: true
      default: function() {
        return [
          { id: 4, name: "张伦", address: "祖安" },
          { id: 5, name: "张俊炜", address: "广东靓仔" },
        ];
      },
    },
  },
  methods: {
      sendValueToParent() {
          /**
           * 参数1：自定义事件的名字，可以随意写，但是不要写系统已经存在的时间，比如 click
           * 参数2：就是你要传递给父组件的值（任意类型）
           */
        //   this.$emit('sendfood',{name:'烧鸭饭',price:15})

        this.$parent.getFoodValue({name:'鸡腿饭',price:20})
      },
      sendValueToChild2() {
        bus.$emit('senddrinks',{name:'草莓啵啵', price:35})
      }
  }
};
</script>
