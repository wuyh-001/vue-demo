<template>
  <div>
    <input type="text" v-model="myValue" />
    <h2>{{ myValue }}</h2>
  </div>
</template>
<script>
import { customRef, ref } from "@vue/reactivity";
export default {
  name: "CustomRefDemo",
  setup() {
    function myRef(value, delay) {
      let timer = null;
      return customRef((track, trigger) => {
        return {
          get() {
            track();
            return value;
          },
          set(newVal) {
            clearTimeout(timer);
            timer = setTimeout(() => {
              value = newVal;
              trigger();
            }, delay);
          },
        };
      });
    }

    let myValue = myRef("abc",500);
    return {
      myValue,
    };
  },
};
</script>