 
 <template>
  <b-row class="mx-3 justify-content-center" :key="renderKey">
    <p v-if="$fetchState.pending">Fetching Objects...</p>
    <p v-else-if="$fetchState.error">An error occurred :(</p>
    <div v-for="obj in objects" v-else :key="obj._id" class="mx-2">
      <!-- Using 'b-card component' & binding 2 props variables -->
      <b-card
        :title="obj.name"
        :img-src="typeImage(obj.type)"
        img-alt="Image"
        img-top
        tag="article"
        style="width: 15rem"
        class="mb-2"
      >
        <b-card-text style="height: 9vh">
          {{ obj.desc }}
        </b-card-text>
        <b-card-text style="height: 9vh">
          {{ obj.found_location }}
        </b-card-text>
        <div class="d-flex justify-content-between align-items-center">
          <b-button
            pill
            v-b-popover.hover.top="`Vous pouvez nous contacter ${obj.contact}`"
            title="Contactez le magasin"
            variant="outline-success"
            >It is your's</b-button
          >
          <b-button pill variant="white" @click="deleteObject(obj._id)">
            <BIconXCircle scale="1.5" variant="danger"></BIconXCircle>
          </b-button>
        </div>
      </b-card>
    </div>
  </b-row>
</template>
<script>
import { BIconXCircle } from "bootstrap-vue";
export default {
  async fetch() {
    // console.log('start fetch',this.objects);
    this.objects = await fetch("http://localhost:3000/get-objects-list", {
      headers: {
        "Access-Control-Allow-Origin": "*",
      },
    })
      .then((res) => res.json())
      .then((res) => res.objects);
    // .catch( (err)=>console.error(err))
    //console.log('after', this.objects)
  },
  components: {
    BIconXCircle,
  },
  data() {
    return {
      // data array - empty to be filled with Mongo data now
      objects: [],
      renderKey: 0,
    };
  },
  methods: {
    typeImage(type) {
      //console.log('in type', type)
      //on selectionne l'image en fonction du type d'objet
      switch (type) {
        case "Communication":
          return require(`../assets/images/communications.png`);
        case "Vetement":
          return require(`../assets/images/location-826x459.jpg`);
        case "Accessoires":
          return require("../assets/images/Fotolia_110243449_S.jpg");
        case "Maroquinerie":
          return require("../assets/images/photo-article.jpg");
        case "Doudou":
          return require("/assets/images/doudous.jpg");
        default:
          return require(`../assets/images/communications.png`);
      }
    },
    async deleteObject(id) {
      //on supprime l'objet de la DDB
      const res = await fetch(`http://localhost:3000/delete-object/${id}`, {
        method: "delete",
        headers: {
          "Access-Control-Allow-Origin": "*",
        },
      })
        .then((res) => res.json())
        .then((res) => console.log("res", res))
        .catch((err) => console.error(err));
      // on supprime l'objet de la page
      const tmp = this.objects.filter((e) => e._id !== id);
      this.objects = [...tmp];
    },
  },
};
</script>

<style lang="postcss">
img {
  height: 150px;
}
</style>
