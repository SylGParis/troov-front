

<template>
  <div>
    <MyNavbar />
    <!-- <NuxtLink to="/">Home page</NuxtLink> -->
    <!-- Using bootstrap container/row/col grid  -->
    <b-container fluid >
      <b-row  class="justify-content-center align-items-center">
        <p class="h1 m-4 text-secondary"> Liste des Objets Trouvés </p>
      </b-row>
      <b-row  class="justify-content-center align-items-center">
       <!-- calling created component    -->
       <ObjectCard />
      </b-row>
    </b-container>
    
</div>
</template>
<script>
export default {
   
  }

</script>
