<template>
  <div id="app">
    <comment-list :comments="comments"></comment-list>
  </div>
</template>

<script>
import json from "./data/data.json";
import CommentList from "./components/CommentList.vue";
export default {
  name: "App",
  components: {
    CommentList,
  },
  data() {
    return {
      comments: [],
    };
  },
  created() {
    this.comments = this.commentListStructure(json, json[0].parentId);
  },
  methods: {
    commentListStructure(data, parentId) {
      return data.reduce((previousValue, currentValue) => {
        if (currentValue.parentId === parentId) {
          const obj = { ...currentValue };
          const children = this.commentListStructure(data, currentValue.id);

          if (children.length) obj.children = children;
          previousValue.push(obj);
        }
        return previousValue;
      }, []);
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
}
</style>
