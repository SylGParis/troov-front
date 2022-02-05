
<template>
  <div
    :style="{ backgroundImage: `url(${bgimage})`, backgroundSize: 'cover', backgroundRepeat: 'noRepeat' ,height: '150vh' }" 
    class="container-fluid justify-center sm:items-center sm:pt-0 px-0"
  >
    <!-- NavBarb component  -->
    <MyNavbar />
    <div class="row mx-auto w-50">
      <p class="mx-auto mt-5 mb-3 h2"> Merci d'avoir retrouvé l'objet!</p>
      <p class="mx-auto  mb-3 h4"> Ajoutez le à la liste des objets trouvés</p>
      <b-card bg-variant="grey" class='w-100'>
        <b-form-group
          label-cols-lg="4"
          label="Descrivez l'Objet Trouvé"
          label-size="lg"
          label-class="font-weight-bold pt-0"
          class="mb-0"
        >
          <b-form-group
            label="Nom de l'objet:"
            label-size="sm"
            label-for="input-1"
            label-cols-sm="4"
            label-align-sm="right"
            label-class="font-weight-bold pt-0"
            class="m-2"
          >
            <b-form-input
              class="m-1"
              placeholder="Quel objet? "
              id="input-1"
              size="sm"
              v-model="name"
              :state="state"
              trim
            ></b-form-input>
          </b-form-group>

          <b-form-group
            label="Type :"
            label-for="input-2"
            label-size="sm"
            label-cols-sm="4"
            label-align-sm="right"
            label-class="font-weight-bold pt-0"
            class="m-2"
          >
            <b-form-select
              class="m-1"
              id="input-2"
              size="sm"
              v-model="selected"
              :options="options"
            ></b-form-select>
          </b-form-group>

          <b-form-group
            label="Où:"
            label-for="input-3"
            label-cols-sm="4"
            label-align-sm="right"
            label-size="sm"
            label-class="font-weight-bold pt-0"
            class="m-2"
          >
            <b-form-input
              class="m-1"
              placeholder="Où l'avez vous trouvé?"
              size="sm"
              id="input-3"
              v-model="found_location"
              :state="state"
              trim
            ></b-form-input>
          </b-form-group>

          <b-form-group
            label="Description :"
            label-for="textarea"
            label-cols-sm="4"
            label-align-sm="right"
            label-size="sm"
            label-class="font-weight-bold pt-0"
            class="m-2"
          >
            <b-form-textarea
              id="textarea"
              class="m-1"
              v-model="desc"
              placeholder="Décrivez en quelques mots les prinicpales caractéristiques..."
              rows="3"
              max-rows="6"
            ></b-form-textarea>
          </b-form-group>

          <b-form-group
            label="Date:"
            label-for="input-3"
            label-cols-sm="4"
            label-align-sm="right"
            label-size="sm"
            label-class="font-weight-bold pt-0"
            class="m-2"
          >
            <b-form-datepicker
              size="sm"
              id="datepicker"
              placeholder="Quand l'avez vous trouvé?"
              v-model="date"
              class="m-1"
            ></b-form-datepicker>
          </b-form-group>

          <b-form-group
            label="Contact:"
            label-for="input-4"
            label-cols-sm="4"
            label-align-sm="right"
            label-size="sm"
            label-class="font-weight-bold pt-0"
            class="m-2"
          >
            <b-form-input
              class="m-1"
              size="sm"
              placeholder="Où peut on vous contacter (email/téléphone)?"
              id="input-4"
              v-model="contact"
              :state="state"
              trim
            ></b-form-input>
          </b-form-group>
        <b-button variant="success">Ajouter l'objet</b-button>
        </b-form-group>
      </b-card>
    </div>
  </div>
</template>
<style >
</style>
<script>
import bgImg from "../assets/images/troov-1920x600.jpg";
export default {
  computed: {
    state() {
      return (
        this.name.length >= 4 ||
        this.found_location.length >= 4 ||
        this.desc.length >= 4 ||
        this.date.length >= 4 ||
        this.contact.length >= 4
      );
    },
    invalidFeedback() {
      if (
        this.name.length > 0 ||
        this.found_location.length >= 0 ||
        this.desc.length >= 0 ||
        this.date.length >= 0 ||
        this.contact.length >= 0
      ) {
        return "Entrez au moins 4 caractères.";
      }
      return "Ce champ ne peut pas être vide.";
    },
  },
  data() {
    return {
      name: "",
      found_location: "",
      desc: "",
      date: "",
      contact: "",
      bgimage: bgImg,
      selected: null,
      options: [
        { value: null, text: "Merci de sélectionner une option" },
        { value: "Communication", text: "Téléphone,tablette,..." },
        { value: "Vetement", text: "Vêtement" },
        { value: "Accessoires", text: "Accessoires (chapeau, gants, ...)" },
        {
          value: "Maroquinerie",
          text: "Sacs, porte-feuille, porte-monnaie...",
        },
        { value: "Doudou", text: "doudou, peluche..." },
        { value: "Autre", text: "Autres" },
      ],
    };
  },
};
</script>
