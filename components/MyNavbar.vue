<template>
  <div>
    <b-navbar toggleable="lg" type="dark" variant="info">
      <b-navbar-brand href="/objectScreen">Objets Trouvés</b-navbar-brand>

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav>
          <b-nav-item href="/addObject">Nouveau</b-nav-item>
          <b-nav-item href="#" disabled>Chercher</b-nav-item>
        </b-navbar-nav>

        <!-- Right aligned nav items -->
        <b-navbar-nav class="ml-auto">
            <b-nav-item href="/">Logout
                <BIconPower class="b-btn text-white m-auto"/> 
            </b-nav-item>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </div>
</template>
<script>
import { BIconPower } from 'bootstrap-vue'
export default {
  components: {
    BIconPower
  }
  };
</script>