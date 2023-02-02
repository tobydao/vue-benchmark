<script setup>
import { shallowRef } from 'vue'
let id = 1;
const dataSource = shallowRef([])

function buildData(count = 1000) {
  var adjectives = ["pretty", "large", "big", "small", "tall", "short", "long", "handsome", "plain", "quaint", "clean", "elegant", "easy", "angry", "crazy", "helpful", "mushy", "odd", "unsightly", "adorable", "important", "inexpensive", "cheap", "expensive", "fancy"];
  var colours = ["red", "yellow", "blue", "green", "pink", "brown", "purple", "brown", "white", "black", "orange"];
  var nouns = ["table", "chair", "house", "bbq", "desk", "car", "pony", "cookie", "sandwich", "burger", "pizza", "mouse", "keyboard"];
  var data = [];

  for (var i = 0; i < count; i++) {
    data.push({ id: id, label: adjectives[random(adjectives.length)] + " " + colours[random(colours.length)] + " " + nouns[random(nouns.length)] });
    id++;
  }
  return data;
}

function random(max) {
  return Math.round(Math.random() * 1000) % max
}

function create(num) {
  id = 1;
  dataSource.value = buildData(num);
}

function add() {
  dataSource.value = dataSource.value.concat(buildData(1000))
}

function clear() {
  dataSource.value = [];
}
</script>

<template>
  <div class="header">
    <h2>Vue Benchmark</h2>
    <hr>
    <div class="btns">
      <button type="button" id="run" @click="create(1000)">Erstelle 1000 Zeilen</button>
      <button type="button" id="runLot" @click="create(10000)">Erstelle 10.000 Zeilen</button>
      <button type="button" id="add" @click="add()">Füge 1000 Zeilen hinzu</button>
      <button type="button" id="clear" @click="clear()">Lösche alle Zeilen</button>
    </div>
    <hr>
  </div>
  <div class="table">
    <table>
      <tr v-for="{ id, label } of dataSource">
        <td>{{ id }}</td>
        <td>{{ label }}</td>
      </tr>
    </table>
  </div>
</template>

<style scoped>
.header h2 {
  text-align: center;
}

.btns {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
}

.btns button {
  padding: 10px
}
</style>
