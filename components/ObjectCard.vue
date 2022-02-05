 
 <template>
 <div class="mx-3 d-flex justify-content-center align-items-center">
  <p v-if="$fetchState.pending">Fetching Objects...</p>
  <p v-else-if="$fetchState.error">An error occurred :(</p>
  <div 
    v-for="obj in objects" 
    v-else
    :key="obj._id"
    class="mx-2 "
  >
  <b-col>
    
      <!-- Using 'b-coard component' & binding 2 props variables --> 
    <b-card
      :title="obj.name"
      :img-src='typeImage(obj.type)'
      img-alt="Image"
      img-top
      tag="article"
      style="max-width: 20rem"
      class="mb-2 d-inline-flex"
    >
      <b-card-text style="height: 5vh">
        {{ obj.desc }}
      </b-card-text>
       <b-card-text style="height: 5vh">
        {{ obj.found_location }}
      </b-card-text>
      <div class="d-flex justify-content-between align-items-center">
      <b-button pill v-b-popover.hover.top="`Vous pouvez nous contacter ${obj.contact}`" title="Contactez le magasin" variant="outline-success">It is your's</b-button>
      <BIconXCircle scale="1.5" variant="danger"></BIconXCircle>
      </div>

    </b-card>
  </b-col>
  </div>
</div>
</template>
<script>
import { BIconXCircle } from 'bootstrap-vue'
export default {
  async fetch() {
    // console.log('start fetch',this.objects);
    this.objects= await fetch ('http://localhost:3000/get-objects-list', {
      headers: { 
        "Access-Control-Allow-Origin": '*'
      }
      })
    .then((res)=>res.json())
    .then((res)=> res.objects)
   // .catch( (err)=>console.error(err))
    console.log('after', this.objects)
 },
  components: {
    BIconXCircle
  },
  data () {
     
    return {
      // data array - empty to be filled with Mongo data now 
      objects: []

    }
  },
  methods: {
    typeImage (type){
      console.log('in type', type)
      //on selectionne l'image en fonction du type d'objet
      switch (type) {
        case 'Communication': 
          return require(`../assets/images/communications.png`);
        case "Vetement" :
          return require(`../assets/images/location-826x459.jpg`);
        case "Accessoires":
          return require('../assets/images/Fotolia_110243449_S.jpg');
        case "Maroquinerie":
          return require('../assets/images/photo-article.jpg');
        case "Doudou":
          return require('/assets/images/doudous.jpg');
        default: 
          return require(`../assets/images/communications.png`);
      }
    },
    
  },
 
};
</script>

<style lang="postcss">
 img {
   height: 150px;
 }
</style>
