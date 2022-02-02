 
 <template>
  <b-col >
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
       {{ card.text}}
      </b-card-text>

      <b-button href="#" variant="primary">Go somewhere</b-button>
    </b-card>
  </b-col>
</template>
 <script>
export default {
  props: {
      card: {
          type: Object,
          default: ()=>{}
      }
  }
  }
</script>

<style>

</style>
