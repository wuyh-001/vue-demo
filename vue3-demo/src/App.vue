<template>
  <div>
    <hello-world @sayFn="sayFn" :title="title">
      <span>默认插槽slot</span>
      <template v-slot:content>具名slot-content</template>
      <template v-slot:footer="parentData">具名作用域slot-footer=={{parentData.childUser.fullName}}</template>
    </hello-world>
    <hr/>
    <!-- WatchDemo -->
    <watch-demo></watch-demo>
    <hr/>
    <ref-demo></ref-demo>
    <hr/>
    <custom-ref-demo></custom-ref-demo>
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import WatchDemo from "./components/WatchDemo.vue";
import RefDemo from "./components/RefDemo.vue";
import CustomRefDemo from "./components/CustomRefDemo.vue";
export default {
  name: "App",
  components: {
    HelloWorld,
    WatchDemo,
    RefDemo,
    CustomRefDemo
  },
  setup() {
    function sayFn(value) {
      alert("parentSayFn");
      console.log("parentSayFn:", value);
    }
    let title = "rose and jack";
    return {
      title,
      sayFn,
    };
  },
};
</script>
 
