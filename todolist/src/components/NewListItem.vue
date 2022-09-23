<template>
  <div class="newli">
    <div>
      {{ msg }}
    </div>
    <label for="newLi">Input new task and press "Enter"</label>
    <input
      type="text"
      v-model.lazy="newLiData"
      id="newLi"
      v-on:keyup.enter="additem"
    />
    <div v-if="LiDataArr">
        <template v-for="(item, index) in LiDataArr">
          <div :key="index" class="li-wrapper">
          <label class="item">
            <input type="checkbox" name="li-check" style="display:none"/>
            <span id="li--check">{{ index }}</span>
          </label>
          <div contenteditable="true" class="list-item item" v-on:focusout="saveChanges">
            {{ item }}
          </div>
          <button class="item delete-btn" :value="index" v-on:click="deleteLi">delete</button>
          </div>
        </template>
    </div>

  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class NewListItem extends Vue {
  @Prop() private msg!: string;
  newLiData = '';
  LiDataArr: string[] = [];
  editFlag = false;
  additem() {
    this.LiDataArr.push(this.newLiData);
  }
  deleteLi(el) {
    let index = el.target.value;
    this.LiDataArr.splice(index,1);
  }
  saveChanges(el) {
    console.log(el.target.innerText)
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
.list-item {
  display: flex;
  margin-left: auto;
  margin-right: auto;
  margin-top: 1em;
  width: 50%;
  border: 0.1em solid rgb(0, 0, 0);
  border-radius: 20px;
  text-indent: 1em;
  height: 20%;
}
#li--check {
  width: 20%;
  height: 20%;
  margin-right: 1em;
  -webkit-appearance: none;
  -moz-appearance: none;
  background: rgb(252, 248, 248);
  outline: teal;
  border: 0.1em solid black;
  transition: 0.2s;
  position: relative;
}

label input[type="checkbox"]:checked + #li--check {
  background: #7F2929;
}
.li-wrapper {
  text-align: center;
}
.item {
  display: inline-block;
  margin-right: -0.25em;
}
.delete-btn {
  margin-left: 1em;
}
</style>
