<template>
  <div class='training'>
    <h1>Math Training. Level {{level + 1}} </h1>
    <hr>
    <div class="progress">
      <div class="progress-bar" :style="styleProgress"></div>
    </div>
    <div class="box">
      <transition name="slide-fade"  
                  mode="out-in"
                  enter-active-class="animated flipInX"
                  leave-active-class="animated flipOutX"
                  :duration="{ enter: 400, leave: 400}"            
      >
        <app-start-screen 
          v-if="state == 'start'"
          @onStart="onStart"
          >
        </app-start-screen>
        <app-question v-else-if="state == 'question'"
                      @success="onQuestionSuccess"
                      @error="onQuestionError"
                      :settings="levels[level]"
        >
                      
        </app-question>
        <app-message v-else-if="state == 'message'"
                    :type="message.type"
                    :text="message.text"
                    @onNext="onNext"
        >

        </app-message>
        <app-result-screen v-else-if="state == 'result'"
                           :stats="stats"
                           @repeat="onStart"
                           @nextLevel="onNextLevel"
        >
        </app-result-screen>
        <div v-else> Unknown state</div>
      </transition>
    </div>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      state: "start",
      stats: {
        success: 0,
        error: 0
      },
      message: {
        type: "",
        text: ""
      },
      questionMax: 5,
      level: 0,
      levels: [
        {
          from: 10,
          to: 40,
          range: 20,
          variants: 2
        },
        {
          from: 100,
          to: 200,
          range: 20,
          variants: 4
        },
        {
          from: 500,
          to: 1000,
          range: 90,
          variants: 6
        }
      ]
    };
  },
  methods: {
    onStart() {
      this.state = "question";
      this.stats.success = 0;
      this.stats.error = 0;
    },
    onQuestionSuccess() {
      this.state = "message";
      this.message.text = "Well done!";
      this.message.type = "success";
      this.stats.success++;
    },
    onQuestionError(msg) {
      this.state = "message";
      this.message.text = msg;
      this.message.type = "warning";
      this.stats.error++;
    },
    onNext() {
      if (this.questDone < this.questionMax) {
        this.state = "question";
      } else {
        this.state = "result";
      }
    },
    onNextLevel() {
      this.level++;
      this.onStart();
    }
  },
  computed: {
    questDone() {
      return this.stats.success + this.stats.error;
    },
    styleProgress() {
      return {
        width: this.questDone / this.questionMax * 100 + "%"
      };
    }
  }
};
</script>

<style scoped>
h1 {
  font-family: "Bitter";
}
.training {
  max-width: 700px;
  margin: 20px auto;
}

.box {
  margin: 10px 0;
}

.progress-bar {
  transition: 0.5s;
}
</style>
