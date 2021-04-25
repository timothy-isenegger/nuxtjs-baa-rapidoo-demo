<template>
  <div class="homepage">
    <section class="jumbotron jumbotron-fluid d-flex align-items-center">
      <div class="container">
        <div class="row">
          <div class="col-12 col-md-6 col-lg-4">
            <h1>Meet Efficiently,
              Online</h1>
            <p class="lead">
              Find out how rapidoo helps you the most.
            </p>
            <nuxt-link to="/steps/1" class="btn btn-primary text-uppercase">Tutorial starten
              <b-icon-arrow-right class="ml-2"></b-icon-arrow-right>
            </nuxt-link>
          </div>
        </div>
      </div>
    </section>
    <div class="container">
      <div class="row">
        <div class="col-12 col-lg-7">
          <section class="explanation explanation-set">
            <h2>Set</h2>
            <p>Bei den Vorbereitungen kommt es besonders auf folgende Punkte an:</p>
            <ol>
              <li>Lorem ipsum dolor sit amet, consectetur</li>
              <li>incididunt ut labore et dolore magna aliqua.</li>
              <li>Ut enim ad minim veniam, quis nostrud</li>
              <li>velit esse cillum dolore eu fugiat nulla pariatur.</li>
            </ol>
          </section>
          <section class="explanation explanation-set">
            <h2>Meet</h2>
            <p>Beim Meeting kommt es besonders auf folgende Punkte an:</p>
            <ol>
              <li>Lorem ipsum dolor sit amet</li>
              <li>incididunt ut labore et dolore magna aliqua.</li>
              <li>Ut enim ad minim veniam, quis nostrud</li>
            </ol>
          </section>
          <section class="explanation explanation-set">
            <h2>Track</h2>
            <p>Nach dem Meeting ist vor dem Meeting - folgende Punkte sind zu beachten:</p>
            <ol>
              <li>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed</li>
              <li>incididunt ut labore et dolore magna aliqua.</li>
              <li>Ut enim</li>
              <li>velit esse cillum dolore eu fugiat nulla</li>
              <li>incididunt ut labore et dolore magna aliqua.</li>
            </ol>
          </section>
        </div>
        <div class="col-12 col-lg-5 d-none d-lg-flex align-items-center">
          <img src="~/assets/images/rapidoo-cloud.png" alt="Rapidoo cloud" class="img-fluid">
        </div>
        <div class="col-12 col-md-8 offset-md-2 mt-5">
          <img src="~/assets/images/rapidoo-cycle.png" alt="Rapidoo cloud" class="img-fluid">
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {}
</script>

<style lang="scss">
.jumbotron {
  background: linear-gradient(rgba(255, 255, 255, 0.5),
    rgba(255, 255, 255, 0.5)),
  url('~assets/images/luke-chesser-48.jpg');
  background-size: cover;
  background-position: center bottom;
  min-height: 80vh;
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
