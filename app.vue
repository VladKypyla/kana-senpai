<template>
  <img class="img" src="./assets/kana-chan.png" alt="">
  <div v-if="selecting" class="card">
    <h2>Options</h2>
    <div class="kana-checkbox">
      <input type="checkbox" v-model="showHiragana">
      <label>Show Hiragana</label>
    </div>
    <div class="kana-checkbox">
      <input type="checkbox" v-model="showKatakana">
      <label>Show Katakana</label>
    </div>
    <h2>Select Kana</h2>
    <div class="row" v-for="row in kanaData">
      <input v-model="row[0].selected" type="checkbox">
      <div class="kana-checkbox" v-for="kana in row" :key="kana.hiragana">
        <label for="{{ kana.hiragana }}">{{ kana.hiragana }}</label>
      </div>
    </div>
    <button class="button" @click="start">スタート</button>
  </div>
  <div v-else class="card">
    <h1 v-if="!showAnswer" class="text">{{currentDisplay}}</h1>
    <h1 v-else class="text" v-if="showAnswer">{{ currentCard.romaji }}</h1>
    <div class="button-container">
      <button class="button" v-if="!showAnswer" @click="toggleAnswer">解答を見る</button>
      <button class="button" v-else @click="getRandomCard">次へ</button>
    </div>
  </div>
</template>

<script>
export default {
data() {
  return {
    kanaData: [
    [
    { hiragana: "あ", katakana: "ア", romaji: "a" },
    { hiragana: "い", katakana: "イ", romaji: "i" },
    { hiragana: "う", katakana: "ウ", romaji: "u" },
    { hiragana: "え", katakana: "エ", romaji: "e" },
    { hiragana: "お", katakana: "オ", romaji: "o" },],
   [ { hiragana: "か", katakana: "カ", romaji: "ka" },
    { hiragana: "き", katakana: "キ", romaji: "ki" },
    { hiragana: "く", katakana: "ク", romaji: "ku" },
    { hiragana: "け", katakana: "ケ", romaji: "ke" },
    { hiragana: "こ", katakana: "コ", romaji: "ko" },],
   [ { hiragana: "さ", katakana: "サ", romaji: "sa" },
    { hiragana: "し", katakana: "シ", romaji: "shi" },
    { hiragana: "す", katakana: "ス", romaji: "su" },
    { hiragana: "せ", katakana: "セ", romaji: "se" },
    { hiragana: "そ", katakana: "ソ", romaji: "so" },],
   [ { hiragana: "た", katakana: "タ", romaji: "ta" },
    { hiragana: "ち", katakana: "チ", romaji: "chi" },
    { hiragana: "つ", katakana: "ツ", romaji: "tsu" },
    { hiragana: "て", katakana: "テ", romaji: "te" },
    { hiragana: "と", katakana: "ト", romaji: "to" },],
   [ { hiragana: "な", katakana: "ナ", romaji: "na" },
    { hiragana: "に", katakana: "ニ", romaji: "ni" },
    { hiragana: "ぬ", katakana: "ヌ", romaji: "nu" },
    { hiragana: "ね", katakana: "ネ", romaji: "ne" },
    { hiragana: "の", katakana: "ノ", romaji: "no" },],
   [ { hiragana: "は", katakana: "ハ", romaji: "ha" },
    { hiragana: "ひ", katakana: "ヒ", romaji: "hi" },
    { hiragana: "ふ", katakana: "フ", romaji: "fu" },
    { hiragana: "へ", katakana: "ヘ", romaji: "he" },
    { hiragana: "ほ", katakana: "ホ", romaji: "ho" },],
   [ { hiragana: "ま", katakana: "マ", romaji: "ma" },
    { hiragana: "み", katakana: "ミ", romaji: "mi" },
    { hiragana: "む", katakana: "ム", romaji: "mu" },
    { hiragana: "め", katakana: "メ", romaji: "me" },
    { hiragana: "も", katakana: "モ", romaji: "mo" },],
   [ { hiragana: "や", katakana: "ヤ", romaji: "ya" },
    { hiragana: "ゆ", katakana: "ユ", romaji: "yu" },
    { hiragana: "よ", katakana: "ヨ", romaji: "yo" },],
   [ { hiragana: "ら", katakana: "ラ", romaji: "ra" },
    { hiragana: "り", katakana: "リ", romaji: "ri" },
    { hiragana: "る", katakana: "ル", romaji: "ru" },
    { hiragana: "れ", katakana: "レ", romaji: "re" },
    { hiragana: "ろ", katakana: "ロ", romaji: "ro" },],
   [ { hiragana: "わ", katakana: "ワ", romaji: "wa" },
    { hiragana: "ゐ", katakana: "ヰ", romaji: "wi" },
    { hiragana: "ゑ", katakana: "ヱ", romaji: "we" },
    { hiragana: "を", katakana: "ヲ", romaji: "wo" },],
  [  { hiragana: "ん", katakana: "ン", romaji: "n" },]
    ],
    currentCard: {},
    showAnswer: false,
    selecting: true,
    showHiragana: false,
    showKatakana: false,
  };
},

methods: {
  start(){
    this.kanaData = this.kanaData.filter(row => row[0].selected).flat(Infinity)
    this.getRandomCard();
    this.selecting = false;
  },
  getRandomCard() {
    this.currentCard = this.kanaData[Math.floor(Math.random() * this.kanaData.length)];
    this.showAnswer = false;
  },
  toggleAnswer() {
    this.showAnswer = !this.showAnswer;
  },
},
computed:{
  currentDisplay(){
    return `${this.showHiragana ? this.currentCard.hiragana : ""} ${this.showKatakana ? this.currentCard.katakana : ""}`
  }
}
};
</script>


<style>
body {
margin: 0;
padding: 0;
font-family: 'Exo 2', sans-serif;
}

.row{
display: flex;
justify-content: flex-start;
gap:0.5rem

}

.img {
position: absolute;
bottom:0;
right: 0;
width: 300px;
}

.card {
background-color: #f5f5f5;
border: none;
border-radius: 5px;
margin: 10% auto;
width: 300px;
padding: 20px;
box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
justify-content: center;
}

.text
{
text-align: center;
margin-bottom: auto;
font-size: 3rem;
line-height: 5rem;
font-weight: bold;
}

.button-container {
display: flex;
justify-content: space-between;
margin-top: 20px; 
}

.button {
margin:auto;
background-color: #ffc107; 
border: none;
border-radius: 5px;
padding: 15px 30px; 
cursor: pointer;
color: #000;
font-weight: bold;
font-size: 16px;
font-family: 'Exo 2', sans-serif; 
transition: all 0.2s ease-in-out;
box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
}

.button:hover {
background-color: #ffb300;
}

</style>
