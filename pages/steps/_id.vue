<template>
<div class="container">
  <h1>{{ step.title }}</h1>
  <div class="row">
    <div class="col-12 col-md-8">
      <div id="step-image-wrapper" class="mb-5 mb-md-3">
        <img :src="require(`~/assets/images/${step.image}`)" class="img-fluid" alt=""/>
        <div v-for="reference in step.references"
             :key="reference.id"
             :style="{top:reference.posY + 'px', left:reference.posX + 'px'}"
             class="popover-wrapper">

          <b-button :id="'referenceTarget' + reference.id"></b-button>

          <b-popover
            :target="'referenceTarget' + reference.id"
            placement="bottom"
            container="step-image-wrapper">

            <small class="d-block text-right">{{reference.id}} von {{ totalNumberOfReferences }}</small>

            <p>{{ reference.description }}</p>
            <div class="d-flex justify-content-between">
              <b-button size="sm" variant="outline-primary" @click="previous(reference.id)"><b-icon-arrow-left></b-icon-arrow-left></b-button>
              <b-button size="sm" variant="primary" @click="next(reference.id)"><b-icon-arrow-right></b-icon-arrow-right></b-button>
            </div>
          </b-popover>
        </div>

      </div>
    </div>
    <div class="col-12 col-md-4">
      <ul class="references">
        <li v-for="reference in step.references" :key="reference.id" :id="'referenceItem' + reference.id" class="references-item" @click="openReference(reference.id)">
          {{ reference.id }} {{ reference.title }}
        </li>
      </ul>
    </div>

    <div class="col-md-8 d-flex justify-content-between mt-4">
      <div v-for="phase in phases" :key="phase.id" class="phase-item text-uppercase" :class="{ 'phase-item-active' : phase.id === activePhase.id}" :id="'phase' + phase.id">
        {{ phase.title }}<b-icon :icon="phase.icon" class="ml-2"></b-icon>
        </div>
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
      phases: jsonData.phases
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
    nextLink() {
      if (parseInt(this.id) >= this.steps.length) {
        return '/workshop';
      } else {
        const nextStep = parseInt(this.id) + 1;
        return `/steps/${nextStep}`;
      }
    },
    prevLink() {
      if (parseInt(this.id) === 1) {
        return '/';
      } else {
        const prevStep = parseInt(this.id) - 1;
        return `/steps/${prevStep}`;
      }
    }
  },
  mounted() {
    this.openReference(parseInt(1));
  },
  methods: {
    openReference(refId) {
      this.$root.$emit('bv::hide::popover');
      const target = 'referenceTarget' + refId;

      window.setTimeout(() => {
        this.$root.$emit('bv::show::popover', target);
      this.highlightReference(refId);
      }, 20)
    },

    highlightReference(refId) {
      this.removeActiveFromReferences();
      document.querySelector(`#referenceItem${refId}`).classList.add('active');
    },

    removeActiveFromReferences() {
      document.querySelectorAll('.references-item').forEach(item => item.classList.remove('active'));
    },

    next(referenceId) {
      if (parseInt(referenceId) === this.step.references.length) {
        this.nextStep();
        return false;
      }

      this.openReference(parseInt(referenceId) + 1);
    },

    previous(referenceId) {
      if (parseInt(referenceId) === 1) {
        this.previousStep();
        return false;
      }

      this.openReference(parseInt(referenceId) - 1);
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
        this.$router.push({
          path: `/steps/${prevStep}`
        });
      }
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
        width: 200px;
        border-top: 1px solid $dark;
        position: absolute;
        left: 80px;
        top: 50%;
        transform: translateY(-50%);
      }

      &:nth-child(2) {
        &:after {
          left: 100px;
        }
      }
    }


    &-active {
      color: $primary;
      font-weight: bold;
    }
  }
</style>
