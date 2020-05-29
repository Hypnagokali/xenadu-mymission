<template>
<div>
  <label class="container">{{ task }}
  <input @change="$emit('update:checked', isChecked)" type="checkbox" v-model="isChecked">
  <span class="checkmark"></span>
</label>
</div>
</template>

<script>
export default {
  name: 'TodoItem',
  props: {
    id: Number,
    task: String,
    checked: Boolean,
  },
  data() {
    return {
      isChecked: this.checked,
    };
  },
  methods: {
    logThis() {
      console.log(this.isChecked);
    },
  },
};
</script>

<style scoped lang="scss">
/* The container */
.container {
  display: block;
  position: relative;
  padding-left: 35px;
  margin-bottom: 12px;
  cursor: pointer;
  font-size: 18px;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

/* Hide the browser's default checkbox */
.container input {
  position: absolute;
  opacity: 0;
  cursor: pointer;
  height: 0;
  width: 0;
}

/* Create a custom checkbox */
.checkmark {
  position: absolute;
  border: solid 1px;
  top: 0;
  left: 0;
  height: 20px;
  width: 20px;
  background-color: #eee;
}

/* On mouse-over, add a grey background color */
.container:hover input ~ .checkmark {
  background-color: #ccc;
}

/* When the checkbox is checked, add a blue background */
.container input:checked ~ .checkmark {
  background-color: green;
}

/* Create the checkmark/indicator (hidden when not checked) */
.checkmark:after {
  content: "";
  position: absolute;
  display: none;
}

/* Show the checkmark when checked */
.container input:checked ~ .checkmark:after {
  display: block;
}

/* Style the checkmark/indicator */
.container .checkmark:after {
  left: 6px;
  top: -1px;
  width: 5px;
  height: 15px;
  border: solid white;
  border-width: 0 4px 4px 0;
  -webkit-transform: rotate(45deg);
  -ms-transform: rotate(45deg);
  transform: rotate(45deg);
}
</style>
