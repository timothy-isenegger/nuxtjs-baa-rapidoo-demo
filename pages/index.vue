<template>
  <div class="homepage">
    <section class="jumbotron jumbotron-fluid d-flex align-items-center">
      <div class="container">
        <div class="row">
          <div class="col-12 col-md-6 col-lg-4">
            <h1>Erreiche mehr mit deinen Meetings!</h1>
            <p class="lead">
              Rapidoo bringt deine Meetings auf ein neues Level! Steigere deine Effizienz, behalte jederzeit den Überblick und liefere schneller Resultate.
            </p>
            <nuxt-link to="/steps/1" class="btn btn-primary text-uppercase">Demo starten
              <b-icon-arrow-right class="ml-2"></b-icon-arrow-right>
            </nuxt-link>
          </div>
        </div>
      </div>
      <div class="chevron-down-wrapper" @click="scrollDown()">
        <b-icon-chevron-compact-down class="icon-chevron-down"></b-icon-chevron-compact-down>
      </div>
    </section>
    <div class="container">
      <div class="row">
        <div class="col-12 col-lg-7">
          <section class="explanation explanation-set">
            <h2>Set</h2>
            <p>Als Erstes, eröffne das Meeting auf Rapidoo, lade die Teilnehmer ein und versende die Agenda.</p>
            <ol>
              <li>Meeting und Agenda erstellen</li>
              <li>Teilnehmende einladen</li>
            </ol>
          </section>
          <section class="explanation explanation-set">
            <h2>Meet</h2>
            <p>Du triffst deine Kollegen und alle To Dos, Entscheidungen und Notizen werden auf Rapidoo festgehalten.</p>
            <ol>
              <li>Notizen und To Dos erfassen</li>
              <li>Protokoll automatisiert verschicken</li>
            </ol>
          </section>
          <section class="explanation explanation-set">
            <h2>Track</h2>
            <p>Nach dem Meeting kannst du alle Aufgaben nachverfolgen und das Protokoll wird automatisch versendet.</p>
            <ol>
              <li>Erledigung der To Dos verfolgen</li>
              <li>Entscheidungen einsehen</li>
              <li>Protokolle kommentieren und genehmigen</li>
            </ol>
          </section>
        </div>
        <div class="col-12 col-lg-5 d-none d-lg-flex align-items-center">
          <img src="~/assets/images/SMT-Clouds.svg" alt="Rapidoo cloud" class="img-fluid">
        </div>
        <div class="col-12 col-md-8 offset-md-2">
          <img src="~/assets/images/SMT-Circle.svg" alt="Rapidoo cloud" class="img-fluid">
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    scrollDown() {
      window.scrollTo({
        top: document.querySelector('.jumbotron').clientHeight + 72,
        left: 0,
        behavior: 'smooth'
      });
    }
  }
}
</script>

<style lang="scss">
.jumbotron {
  background: linear-gradient(rgba(255, 255, 255, 0.5),
    rgba(255, 255, 255, 0.5)),
  url('~assets/images/luke-chesser-48.jpg');
  background-size: cover;
  background-position: center bottom;
  min-height: 80vh;
  position: relative;
}

.chevron-down-wrapper {
  bottom: 0;
  cursor: pointer;
  left: 50%;
  padding: 1rem 0;
  position: absolute;
  text-align: center;
  transform: translateX(-50%);
  width: 100%;
}

.icon-chevron-down {
  font-size: 3rem;
}

h1 {
  font-size: 32px;
}

.demo-benefits {
  margin-top: 4rem;

  .title {
    font-size: 18px;
    margin-top: 1.5rem;
  }
}

.explanation {
  margin-top: 4rem;
}
</style>
