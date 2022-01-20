<template>
  <li class="comment-box">
    <p class="comment-box__user">{{ getFullName }}</p>
    <p class="comment-box__description">{{ getCommentDescription }}</p>

    <ul
      class="comment-box__children"
      v-if="comment.children && comment.children.length"
    >
      <comment-box
        v-for="child in comment.children"
        :key="child.id"
        :comment="child"
      ></comment-box>
    </ul>
  </li>
</template>

<script>
export default {
  name: "CommentBox",
  props: {
    comment: {
      type: Object,
      default: () => {},
    },
  },
  computed: {
    getFullName() {
      return `${this.comment.user.firstName} ${this.comment.user.lastName}`;
    },

    getCommentDescription() {
      return this.comment.info.description;
    },
  },
};
</script>

<style lang="sass">
.comment-box
  list-style: none
  padding: 0
  margin: 0

  &__user
    font-weight: bold

  &__children
    margin-left: 16px
    padding: 0
</style>