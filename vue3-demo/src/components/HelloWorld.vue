<template>
  <div>
    <h1>父级传递的数据</h1>
    <h2>{{ title }}</h2>
    <button @click="testFn">测试调用父级传递的函数</button>
	<br/>
    <slot name="header"></slot>
	<br/>
	<slot name="content"/>
	<br/>
	<slot name="footer" :childUser="person"/>
	<br/>
    <slot></slot>
    <hr />
    <h1>组件内部的内容</h1>
    <span>{{ name }}--{{ age }}</span>
    <button @click="sayName">请点击</button>
    <hr />

    <input type="text" v-model="person.firstName" />
    <input type="text" v-model="person.lastName" />
    <input type="text" v-model="person.fullName" />
  </div>
</template>

<script>
import { ref, reactive, computed } from "vue";
export default {
  name: "App",
  props: ["title"],
  emits: ["sayFn"],
  setup(props, context) {
    // 基本类型数据
    let name = ref("jack");
    let age = ref(20);

    // 引用类型数据
    let person = reactive({
      firstName: "张",
      lastName: "三",
    });

    //  计算属性
    person.fullName = computed({
      get() {
        return person.firstName + "-" + person.lastName;
      },
      set(value) {
        let newName = value.split("-");
        person.firstName = newName[0];
        person.lastName = newName[1];
      },
    });

    function sayName() {
      name.value = "rose";
      age.value = 40;
    }

    //
    function testFn() {
      context.emit("sayFn", 666);
    }

    return {
      name,
      age,
      person,
      sayName,
      testFn,
    };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
h1,
h2,
p {
  padding: 2px;
  margin: 2px;
}
</style>
