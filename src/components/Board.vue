<script setup>
import { ref, computed } from 'vue';

//implementare la logica e calcolare il vincitore
const calculateWinner = (squares) => {
  const lines = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6],
  ];
  for (let i = 0; i < lines.length; i++) {
    const [a, b, c] = lines[i];
    if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
      return squares[a];
    }
  }
  return null;
};

 // stato giocatore e griglia
    const player = ref('X');
    const squares = ref([
      ['', '', ''],
      ['', '', ''],
      ['', '', ''],
    ]);

    const winner = computed(() => calculateWinner(squares.value.flat()));

    //determinare come effettuare una mossa 
    const move = (x, y) => {
      if (winner.value || squares.value[x][y]) return;
      squares.value[x][y] = player.value;
      player.value = player.value === 'X' ? 'O' : 'X';
    };

    //reset del gioco
    const reset = () => {
      player.value = 'X';
      squares.value = [
        ['', '', ''],
        ['', '', ''],
        ['', '', ''],
      ];
    };

</script>

<template>

<div class="container">

<h1>Tris Game</h1>
<h2>Player Move: {{ player }}</h2>

<div v-for="(row, x) in 3" :key="x" class="row">
<button 
v-for="(cell, y) in 3" 
:key="y" 
class="square" 
@click="move(x, y)">
{{ squares[x][y] }}
</button>

</div>
</div>

<button @click="reset" class="button-reset">Reset Game</button>

<h2 v-if="winner" class="finalwinner">
player '{{ winner }}' wins! </h2>

</template>
   

<style scoped>
h1{
 color: white;
 font-family: 'Jersey 10';
 font-size: 65px;
 margin-top: 20px;
 display: flex;
 justify-content: center;
}

h2{
    color: white;
    font-size: 28px;
    display: flex;
    justify-content: center;
    margin-top: 30px;
    margin-bottom: 20px;
}

.square {
  background-color: grey;
  border: 1px solid black;
  float: left;
  font-size: 70px;
  font-weight: bold;
  height: 110px;
  width: 110px;
  color: white;
  text-align: center;
  display: flex;
  justify-content: center;
 
}

.button-reset{
    margin-top: 20px;
    margin-bottom: 5px;
    padding: 10px 15px;
    font-size: 23px;
    font-family: Arial, Helvetica, sans-serif;
    margin-right: -5px;  
    border-radius: 15px;
    border: 1px black;
    color: white;
    background-color: #b61aae;
  
}

.button-reset:hover{
    background-color: #b61aae;
}
 
.finalwinner{
    font-family:'jersey 10';
    font-size: 60px;
    color: white;
    display: flex;
    justify-content: center;
    margin-top: -1px;
}

</style>
   

  