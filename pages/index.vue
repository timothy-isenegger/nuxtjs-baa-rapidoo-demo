<template>
  <div class="container">
    <h1>Rapidoo Demo</h1>
    <p>Rapidoo kennenlernen und die eigene Meetingeffizienz gleichzeitig steigern? Mit der Rapidoo Demo ist das kein Problem! Starte jetzt und sichere dir im anschliessenden Workshop eine effizienzsteigernde Überraschung!</p>
    <section class="demo-benefits">
      <div class="row">
        <div class="col-12 col-md-4 text-center text-uppercase mb-4">
          <b-icon-eye-fill font-scale="3.5"></b-icon-eye-fill>
          <div class="title">
            Live Rapidoo Vorschau
          </div>
        </div>
        <div class="col-12 col-md-4 text-center text-uppercase mb-4">
          <b-icon-list-ol font-scale="3.5"></b-icon-list-ol>
          <div class="title">
            Step by Step Anleitung
          </div>
        </div>
        <div class="col-12 col-md-4 text-center text-uppercase mb-4">
          <b-icon-gift-fill font-scale="3.5"></b-icon-gift-fill>
          <div class="title">
            Überraschung
          </div>
        </div>
      </div>
      <div class="text-center">
        <nuxt-link to="/steps/1" class="btn btn-primary">Demo starten
          <b-icon-arrow-right class="ml-2"></b-icon-arrow-right>
        </nuxt-link>
      </div>
    </section>

    <section class="explanation explanation-set">
      <div class="row">
        <div class="col-12 col-md-8">
          <h2>Set</h2>
          <p>Bei den Vorbereitungen kommt es besonders auf folgende Punkte an:</p>
          <ol>
            <li>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor</li>
            <li>incididunt ut labore et dolore magna aliqua.</li>
            <li>Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate</li>
            <li>velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.</li>
          </ol>
        </div>
        <div class="col-12 col-md-4 d-flex align-items-center">
          <b-icon-star font-scale="5"></b-icon-star>
        </div>
      </div>
    </section>
    <section class="explanation explanation-set">
      <div class="row">
        <div class="col-12 col-md-2 offset-md-2 d-flex align-items-center">
          <b-icon-briefcase font-scale="5"></b-icon-briefcase>
        </div>
        <div class="col-12 col-md-8">
          <h2>Meet</h2>
          <p>Beim Meeting kommt es besonders auf folgende Punkte an:</p>
          <ol>
            <li>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor</li>
            <li>incididunt ut labore et dolore magna aliqua.</li>
            <li>Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip</li>
          </ol>
        </div>
      </div>
    </section>
    <section class="explanation explanation-set">
      <div class="row">
        <div class="col-12 col-md-8">
          <h2>Track</h2>
          <p>Nach dem Meeting ist vor dem Meeting - folgende Punkte sind zu beachten:</p>
          <ol>
            <li>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor</li>
            <li>incididunt ut labore et dolore magna aliqua.</li>
            <li>Ut enim</li>
            <li>velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat</li>
            <li>incididunt ut labore et dolore magna aliqua.</li>
          </ol>
        </div>
        <div class="col-12 col-md-4 d-flex align-items-center">
          <b-icon-link font-scale="5"></b-icon-link>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
export default {}
</script>

<style lang="scss">
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
