<template>
  <div>
      <span>姓名：{{name}}</span>
      <span>年龄：{{age}}</span>
      <span>薪资{{job.salary}}</span>
      <hr/>
      <button @click="name+='^'">修改姓名</button>
      <button @click="age+=10">修改年龄</button>
      <button @click="job.salary+=2">修改薪资</button>
  </div>
</template>
<script>
import { reactive, toRef, toRefs } from "vue";
export default {
  name: "RefDemo",
  setup() {
    let person = reactive({
      name: "张三",
      age: 20,
      sex:'woman',
      job: {
        salary: 30,
      }
    });
    // toRef  操作一个属性
    let p1=toRef(person,'name');
    console.log(p1.value)

    return {
      person,
      name:toRef(person,'name'),
      ...toRefs(person),
    };
  },
};
</script>