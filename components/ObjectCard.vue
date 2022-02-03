 
 <template>
  <b-col>
      <!-- Using 'b-coard component' & binding 2 props variables -->
    <b-card
      :title="card.title"
      :img-src="card.urlImg"
      img-alt="Image"
      img-top
      tag="article"
      style="max-width: 20rem"
      class="mb-2 d-inline-flex"
    >
      <b-card-text>
        {{ card.text }}
      </b-card-text>
      <div class="d-flex justify-content-between align-items-center">
      <b-button pill href="#" variant="outline-success">Go somewhere</b-button>
      <BIconXCircle scale="1.5" variant="danger"></BIconXCircle>
      </div>

    </b-card>
  </b-col>
</template>
<script>
import { BIconXCircle } from 'bootstrap-vue'
export default {
  components: {
    BIconXCircle
  },
    // defining props type 
  props: {
    card: {
      type: Object,
      default: () => {},
    },
  },
};
</script>

<style>
</style>
