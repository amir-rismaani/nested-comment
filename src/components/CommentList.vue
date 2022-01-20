<template>
  <div class="comments">
    <ul class="comment-list" v-if="comments.length">
      <comment-box v-for="comment in comments" :key="comment.id" :comment="comment" class="root-comment"></comment-box>
    </ul>
    <empty-list v-else/>
  </div>
</template>

<script>
import CommentBox from "./CommentBox.vue";
import EmptyList from "./EmptyList.vue";
export default {
  name: "CommentList",
  props: {
    comments: {
      type: Array,
      default: () => [],
    },
  },
  components: {
    CommentBox,
    EmptyList,
  },
  methods: {
    isParent(comment) {
      return !comment.parentId;
    },
  },
};
</script>

<style lang="sass" scoped>
.comment-list
    margin: 0
    padding: 0

    .root-comment
        &:not(:first-child) 
          border-top: 1px solid #eeeeee

</style>