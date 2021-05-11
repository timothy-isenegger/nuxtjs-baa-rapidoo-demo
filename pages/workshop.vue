<template>
  <div class="container">
    <h1>Meeting Novize oder Experte?</h1>
    <div class="row">
      <div class="col-12 col-md-7">
        <div class="mb-4 font-italic small">
          <p>Anleitung:</p>
          <p>Klicke auf eine der Boxen und halte die linke Maustaste gedrückt. Ziehe die Box an die von dir gewünschte Stelle und lasse die Maustaste wieder los. Sobald du mit der Reihenfolge zufrieden bist, klicke rechts auf "Jetzt prüfen".</p>
        </div>
        <div class="workshop-game-background mb-4 mb-md-0" :class="{completed: gameCorrect}">
          <draggable v-model="steps" group="people" @start="drag=true" @end="drag=false">
            <div v-for="step in steps" :key="step.id" class="workshop-game-step">{{ step.name }}</div>
          </draggable>
        </div>
      </div>
      <div class="col-12 col-md-5 col-lg-4 offset-lg-1">
        <section v-if="!gameCorrect">
          <p>Hast du bei der Einführung in Rapidoo gut aufgepasst? Dann wird die folgende Aufgabe ein Kinderspiel für dich sein.</p>
          <p>Bringe die Schritte eines Meetings auf der linken Seite in die von Rapidoo vorgesehene Reihenfolge. Schaffst du es im ersten Anlauf, die Reihenfolge korrekt darzustellen? Es erwartet dich ein tolles Überraschungsgeschenk, mit welchem du in jedem Meeting glänzen wirst.</p>
          <p v-if="gameChecked" class="text-black">Leider stimmt die von dir gewählte Reihenfolge noch nicht ganz. Versuche es noch einmal!</p>
          <div class="text-right">
            <button class="btn btn-primary" v-on:click="checkWorkshopGame()">
              <span v-if="!gameChecked">Jetzt prüfen</span>
              <span v-else>Erneut prüfen</span>
            </button>
          </div>
        </section>
        <section v-if="gameCorrect">
          <p>Du hast den Rapidoo Workshop erfolgreich absolviert. Starte jetzt mit deinem ersten Meeting bei Rapidoo und steigere deine Effizienz!</p>
          <a href="https://app.rapidoo.com/index.php?id=127" title="Neues Meeting" target="_blank" class="btn btn-primary d-inline-block mb-4">Meeting erstellen</a>
          <p>Du machst deine Meetings nach wie vor auf Papier? Hier kannst du eine kurze Checkliste herunterladen, die dich bei deinen Meetings optimal unterstützt.<br/></p>
          <a href="/sample.pdf" title="Checkliste" target="_blank">Checkliste herunterladen</a>
        </section>
      </div>
      <div class="col-12">
        <b-button variant="outline-secondary" @click="navigateToLastStep()" class="mt-4">
          zurück
        </b-button>
      </div>
    </div>
  </div>
</template>

<script>
import draggable from 'vuedraggable';
import jsonData from 'assets/data.json';

export default {
  name: "workshop",
  components: {
    draggable
  },
  data() {
    return {
      steps: jsonData.gameSteps,
      gameChecked: false,
      gameCorrect: false,
    }
  },
  created() {
    this.shuffle(this.steps);
  },
  methods: {
    checkWorkshopGame() {
      this.gameChecked = true;
      this.gameCorrect = true;
      let counter = 1;
      let validationClass = '';

      const stepElements = document.querySelectorAll('.workshop-game-step');
      this.steps.forEach((item, index) => {
        if (item.id === counter) {
          validationClass = 'is-correct';
        } else {
          validationClass = 'is-incorrect';
          this.gameCorrect = false;
        }

        stepElements[index].classList.remove('is-correct', 'is-incorrect');
        stepElements[index].classList.add(validationClass);

        counter++;
      });
    },

    shuffle(array) {
      for (let i = array.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [array[i], array[j]] = [array[j], array[i]];
      }
      return array;
    },
    navigateToLastStep() {
      window.localStorage.setItem('showLastReference', '1');
      this.$router.push({
        path: '/steps/6'
      })
    }
  }
}
</script>

<style lang="scss" scoped>
@import "assets/scss/variables";

h1 {
  margin-top: 3rem;
}

.workshop-game-background {
  background-color: white;
  padding: 2rem;
  min-height: 50vh;

  &.completed {
  pointer-events: none;
  }
}

.workshop-game-step {
  background-color: #E0E0E0;
  border: 1px solid transparent;
  box-shadow: 0 2px 2px rgba(0, 0, 0, 0.15);
  cursor: grab;
  margin-bottom: 10px;
  padding: 15px;
  transition: all .2s ease-in-out;

  &:last-child {
    margin-bottom: 0;
  }

  &:hover {
    box-shadow: 0 3px 3px rgba(0, 0, 0, .25);
  }

  &.sortable-chosen {
    cursor: grabbing;
  }
}

.is-correct {
  background-color: rgba($success, .25);
}

.is-incorrect {
  background-color: rgba($danger, .25);
}

.text-black {
  color: #000;
}
</style>
