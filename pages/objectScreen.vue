

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
       <!-- calling created component & maping on data array   -->
       <ObjectCard 
          v-for="obj in objects" 
          :key="obj.title"
          :card="obj" 
          class="mx-3 align-self-stretch"
        />
      </b-row>
    </b-container>
    
</div>
</template>
<script>
export default {
  data () {
    return {
      // data array - static data now but will be replace by fetch result 
      objects: [{
        title: "Objet1",
        urlImg:'https://picsum.photos/600/300/?image=25',
        text:"Some quick example text to add on the card to describe the object."
      },
      {
        title: "Objet2",
        urlImg:'https://picsum.photos/600/300/?image=25',
        text:"Some quick second desc to add on the card to describe the object."
      },
      {
        title: "Objet3",
        urlImg:'https://picsum.photos/600/300/?image=25',
        text:"Some quick example text to add on the card to describe the object."
      }
      ]
    }
  }
}
</script>
