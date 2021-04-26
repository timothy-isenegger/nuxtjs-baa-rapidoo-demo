<template>
  <div class="container">
    <h1>{{ step.title }}</h1>
    <div class="row">
      <div class="col-12 col-md-8">
        <div id="step-image-wrapper" class="mb-5 mb-md-3">
          <img :src="require(`~/assets/images/${step.image}`)" class="img-fluid" alt=""/>
          <div v-for="reference in step.references"
               :key="reference.id"
               :data-posx="reference.posX"
               :data-posy="reference.posY"
               :data-posxsm="reference.posXsm"
               :data-posysm="reference.posYsm"
               :data-posxmd="reference.posXmd"
               :data-posymd="reference.posYmd"
               :data-posxlg="reference.posXlg"
               :data-posylg="reference.posYlg"
               :data-posxxl="reference.posXxl"
               :data-posyxl="reference.posYxl"
               class="popover-wrapper">

            <b-button :id="'referenceTarget' + reference.id"></b-button>

            <b-popover
              :target="'referenceTarget' + reference.id"
              placement="bottom"
              container="step-image-wrapper">

              <small class="d-block text-right">{{ reference.order }} von {{ totalNumberOfReferences }}</small>

              <p>{{ reference.description }}</p>
              <div class="d-flex justify-content-between">
                <b-button size="sm" variant="outline-primary" @click="previous(reference.order)">
                  <b-icon-arrow-left></b-icon-arrow-left>
                </b-button>
                <b-button size="sm" variant="primary" @click="next(reference.order)">
                  <b-icon-arrow-right></b-icon-arrow-right>
                </b-button>
              </div>
            </b-popover>
          </div>

        </div>
      </div>
      <div class="col-12 col-md-4">
        <ul class="references">
          <li v-for="reference in step.references" :key="reference.id" :id="'referenceItem' + reference.id" class="references-item" @click="openReference(reference.order)">
            {{ reference.order }} {{ reference.title }}
          </li>
        </ul>
      </div>

      <div class="col-md-8 d-flex justify-content-between mt-4">
        <b-button v-for="phase in phases"
                  :key="phase.id"
                  :class="{ 'phase-item-active' : phase.id === activePhase.id}"
                  :id="'phase' + phase.id"
                  @click="goToPhase(phase.id)"
                  variant="link"
                  class="phase-item text-uppercase">
          {{ phase.title }}
          <b-icon :icon="phase.icon" class="ml-2"></b-icon>
        </b-button>
      </div>
    </div>
  </div>
</template>

<script>
import jsonData from 'assets/data.json';

export default {
  data() {
    return {
      id: this.$route.params.id,
      steps: jsonData.steps,
      phases: jsonData.phases,
      screenSize: ''
    }
  },
  computed: {
    step() {
      return this.steps.find(step => step.id === this.id);
    },
    activePhase() {
      return this.phases.find(phase => phase.id === this.step.phaseId);
    },
    totalNumberOfReferences() {
      return this.step.references.length;
    },
  },
  mounted() {
    this.screenSize = this.setScreensize(window.innerWidth);
    let referenceId = 1;
    if (window.localStorage.getItem('showLastReference') === '1') {
      referenceId = this.step.references.length;
      window.localStorage.setItem('showLastReference', '0');
    }
    window.setTimeout(() => {
      this.positionReferencesForScreensize(this.screenSize);
      this.openReference(parseInt(referenceId));
    }, 20)
  },
  methods: {
    openReference(refId) {
      this.$root.$emit('bv::hide::popover');
      const target = 'referenceTarget' + refId;

      this.$root.$emit('bv::show::popover', target);
      this.highlightReference(refId);
    },

    highlightReference(refId) {
      this.removeActiveFromReferences();
      document.querySelector(`#referenceItem${refId}`).classList.add('active');
    },

    removeActiveFromReferences() {
      document.querySelectorAll('.references-item').forEach(item => item.classList.remove('active'));
    },

    next(referenceOrder) {
      if (parseInt(referenceOrder) === this.step.references.length) {
        this.nextStep();
        return false;
      }

      this.openReference(parseInt(referenceOrder) + 1);
    },

    previous(referenceOrder) {
      if (parseInt(referenceOrder) === 1) {
        this.previousStep();
        return false;
      }

      this.openReference(parseInt(referenceOrder) - 1);
    },

    nextStep() {
      if (parseInt(this.id) >= this.steps.length) {
        this.$router.push({
          path: '/workshop'
        });
      } else {
        const nextStep = parseInt(this.id) + 1;
        this.$router.push({
          path: `/steps/${nextStep}`
        });
      }
    },

    previousStep() {
      if (parseInt(this.id) === 1) {
        this.$router.push({
          path: '/',
        });
      } else {
        const prevStep = parseInt(this.id) - 1;
        window.localStorage.setItem('showLastReference', '1');
        this.$router.push({
          path: `/steps/${prevStep}`
        });
      }
    },
    goToPhase(phaseId) {
      console.log(phaseId);
      const step = this.steps.find(step => step.phaseId === phaseId);
      if (step === undefined) {
        window.alert('No step found for this phase!')
        return false;
      }
      this.$router.push({
        path: `/steps/${step.id}`
      });
    },
    setScreensize(actScreensize) {
      if (actScreensize >= 1200) {
        return 'xl';
      }
      if (actScreensize >= 992) {
        return 'lg';
      }
      if (actScreensize >= 768) {
        return 'md';
      }
      if (actScreensize >= 576) {
        return 'sm';
      }
      return '';
    },
    positionReferencesForScreensize(screensize) {
      const positionX = `data-posx${screensize}`;
      const positionY = `data-posy${screensize}`;
      document.querySelectorAll('.popover-wrapper').forEach((popover) => {
        console.log(popover.getAttribute(positionX))
        popover.style.top = popover.getAttribute(positionY) + 'px';
        popover.style.left = popover.getAttribute(positionX) + 'px';
      })
      console.log('set screensize for ' + screensize);
    }
  }
}
</script>

<style lang="scss">
@import '~/assets/scss/variables';
@import '~/node_modules/bootstrap/scss/functions';
@import '~/node_modules/bootstrap/scss/variables';
@import '~/node_modules/bootstrap/scss/mixins';
@import '~/node_modules/bootstrap/scss/grid';

h1 {
  margin-top: 3rem;
  margin-bottom: 1.5rem;
}

.references {
  list-style: none;
  padding-left: 0;
}

.references-item {
  background-color: white;
  border: 2px solid white;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.25);
  cursor: pointer;
  margin-bottom: .5rem;
  padding: .5rem 1rem;
  transition: all .2s ease-in-out;

  &.active, &:hover, &:focus {
    border-color: #1E648C;
  }
}

#step-image-wrapper {
  position: relative;
}

.popover-wrapper {
  position: absolute;
}

.popover-wrapper .btn {
  opacity: 0;
}

.phase-item {
  position: relative;

  @include media-breakpoint-up(xl) {
    &:not(:last-child):after {
      content: '';
      display: inline-block;
      width: 150px;
      border-top: 1px solid $dark;
      position: absolute;
      left: 125px;
      top: 50%;
      transform: translateY(-50%);
    }

    &:nth-child(2) {
      &:after {
        left: 145px;
      }
    }
  }

  &-active {
    color: $primary;
    font-weight: bold;
  }

  &:hover, &:focus {
    text-decoration: none;
  }
}
</style>
