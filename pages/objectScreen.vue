

<template>
  <div>
    <NuxtLink to="/">Home page</NuxtLink>
    <b-container fluid class="bv-example-row">
      <b-row  class="flex-fill justify-content-center align-items-center">
       <ObjectCard 
          v-for="obj in objects" 
          :key="obj.title"
          :card="obj" 
          class="mx-3"
        />
      </b-row>
    </b-container>
    
</div>
</template>
<script>
export default {
  data () {
    return {
      objects: [{
        title: "Objet1",
        urlImg:'https://picsum.photos/600/300/?image=25',
        text:"Some quick example text to add on the card to describe the object."
      },
      {
        title: "Objet2",
        urlImg:'https://picsum.photos/600/300/?image=25',
        text:"Some quick second object desc to add on the card to describe the object."
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
