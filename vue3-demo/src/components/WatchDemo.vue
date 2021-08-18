<template>
  <div>
    <h2>watch</h2>
    <p>{{ sum }}</p>
    <button @click="sum++">点击</button>
    <hr />
    <span @click="person.singer += '~'">{{ person.singer }}</span>
    @@@
    <span @click="person.song += '^'">{{ person.song }}</span>
    <span @click="person.job.job1.money++">{{ person.job.job1.money }}</span>
  </div>
</template>
<script>
import { reactive, ref, watch } from "vue";
export default {
  name: "WatchDemo",
  setup() {
    // 基础数据类型的watch  第一个参数可以是个数组，即需要watch的数据
    let sum = ref(0);
    watch(
      sum,
      (newVal, oldVal) => {
        console.log("sum:", newVal, oldVal);
      },
      {
        immediate: true,
      }
    );
    let person = reactive({
      singer: "周杰伦",
      song: "半岛铁盒",
      age: 36,
      job:{
          job1:{
              money:20
          }
      }
    });
    // 获取不到oldvalue,且deep默认是true并且不能改为false
    // watch(
    //   person,
    //   (newVal, oldVal) => {
    //     console.log("person:", newVal, oldVal);
    //   },
    //   {
    //     immediate: true,
    //   }
    // );

    /*
    监视对象中的某一个属性的改变,监视多个时，传入数组
    */
    watch(
      () => person.singer,
      (newVal, oldVal) => {
        console.log("person.singer:", newVal, oldVal);
      }
    );
    watch(
      [() => person.singer,() => person.song],
      (newVal, oldVal) => {
        console.log("person.singer | song:", newVal, oldVal);
      }
    );

     watch(
      person.job,
      (newVal, oldVal) => {
        console.log("person.job:", newVal, oldVal);
      },
      {
        deep:true
      }
    );

    return {
      sum,
      person,
    };
  },
};
</script>
