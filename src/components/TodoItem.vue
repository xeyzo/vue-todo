<template lang="html">
  <div class="collection-item">
    <div class="row">
      <div class="col s11">
        <div class="content" :class="{ 'is-completed' : todo.completed }" @click="completedToggle()">
          <div class="row">
            <div class="col s1">
              <a><i class="material-icons">{{ checkBoxToggle() }}</i></a>
            </div>
            <div class="col s11">
              <div class="title">{{ todo.title }}</div>
            </div>
          </div>
        </div>
      </div>
      <div class="col s1">
        <div class="actions" :class="{ 'is-completed' : todo.completed }">
          <template v-if="checkStarTrashToggle() == 'delete'">
            <a class="secondary-content" @click="$emit('del-todo', todo.id)">
              <i class="material-icons">{{ checkStarTrashToggle() }}</i>
            </a>
          </template>
          <template v-if="checkStarTrashToggle() == 'star'">
            <a class="secondary-content" @click="isStarred = !isStarred">
              <i class="material-icons star">{{ checkStarTrashToggle() }}</i>
            </a>
          </template>
          <template v-if="checkStarTrashToggle() == 'star_border'">
            <a class="secondary-content" @click="isStarred = !isStarred">
              <i class="material-icons star_border">{{ checkStarTrashToggle() }}</i>
            </a>
          </template>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props: ['todo'],
  data() {
    return {
      isStarred: false
    }
  },
  methods: {
    completedToggle: function() {
      this.todo.completed = !this.todo.completed;
    },
    checkBoxToggle: function() {
      if (this.todo.completed == true) {
        return 'check_box'
      } else {
        return 'check_box_outline_blank'
      }
    },
    checkStarTrashToggle: function() {
      if (this.todo.completed == true) {
        return 'delete'
      } else {
        if (this.isStarred == true) {
          return 'star'
        } else {
          return 'star_border'
        }
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.collection-item {
  border-color: #e5e8ef;
  padding: 12px 0 12px 0;

  .row {
    margin: 0;

    .col {
      padding: 0;
    }
  }
}
.actions, .content {
  cursor: pointer;

  .material-icons {
    color: #e5e8ef;

    &.star {
      color: #ffc00c;
    }

    &.star_border {
      color: #ffc00c;
    }
  }
}
.title {
  color: #4f4f4f;
}
.is-completed {
  .title {
    color: #caced6;
    text-decoration: line-through;
  }

  .material-icons {
    color: #caced6;
  }
}

</style>
