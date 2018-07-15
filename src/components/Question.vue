
<template>
    <div class="alert">
        <h3>{{ x }} + {{ y }} = ? </h3>
        <hr>
        <div class="buttons">
            <button class="answer-btn"
                    v-for="number in answers" :key="number"
                    @click="onAnswer(number)"
            >
                {{ number }}
            </button>
        </div>
    </div>
    
</template>

<script>
export default {
  props: ["settings"],
  data() {
    return {
      x: mtRand(this.settings.from, this.settings.to),
      y: mtRand(this.settings.from, this.settings.to)
    };
  },
  computed: {
    correctAnswer() {
      return this.x + this.y;
    },
    answers() {
      let results = [this.correctAnswer];

      while (results.length < this.settings.variants) {
        let num = mtRand(
          this.correctAnswer - this.settings.range,
          this.correctAnswer + this.settings.range
        );

        if (results.indexOf(num) === -1) {
          results.push(num);
        }
      }

      return results.sort(() => {
        return Math.random() > 0.5;
      });
    }
  },
  methods: {
    onAnswer(num) {
      if (num == this.correctAnswer) {
        this.$emit("success");
      } else {
        this.$emit("error", `${this.x} + ${this.y} = ${this.correctAnswer}!`);
      }
    }
  }
};

function mtRand(min, max) {
  let diff = max - min;
  return Math.floor(Math.random() * (diff + 1)) + min;
}
</script>

<style scoped>
h3 {
  text-align: center;
}
.alert {
  padding-top: 20px;
  background-color: #eee;
}

.buttons {
  display: flex;
  justify-content: space-around;
}
.answer-btn {
  background-color: transparent;
  border: solid 2px rgb(17, 187, 17);
  color: rgb(17, 187, 17);
  border-radius: 25%;
  padding: 5px;
  font-weight: bold;
}
.answer-btn:hover {
  background-color: rgb(17, 187, 17);
  color: white;
  cursor: pointer;
  transition: 0.5s;
  transform: scale(1.2) rotate(360deg) skewX(-15deg);
  border-radius: 0%;
  transition: 0.5s;
}
</style>

