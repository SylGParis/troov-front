
<template>
  <b-container
    fluid
    :style="{
      backgroundImage: `url(${bgimage})`,
      height: '100vh',
      backgroundSize: 'cover',
    }"
    class="items-center m-0 px-0 sm:pt-0"
  >
    <!-- NavBarb component  -->
    <MyNavbar />
    <!-- Sign Up  Card  -->
    <b-row
      cols="3"
      align-h="center"
      align-v="center"
      class="m-5"
      style="height: 80vh"
    >
      <b-card
        bg-variant="transparent"
        class="d-flex mx-3 p-1"
        style="height: 30vh"
      >
        <b-form-group
          label-cols-lg="4"
          label="Sign-Up"
          label-size="lg"
          label-class="font-weight-bold my-auto pt-0"
          class="mb-1 mx-2"
        >
          <b-form-group
            label="Nom :"
            label-size="sm"
            label-for="input-1"
            label-cols-sm="4"
            label-align-sm="right"
            label-class="font-weight-bold my-auto px-0 pt-0"
            class="m-2"
          >
            <b-form-input
              class="m-1"
              placeholder="Votre nom "
              id="input-1"
              size="sm"
              v-model="userName"
              :state="state"
              trim
            ></b-form-input>
          </b-form-group>
          <b-form-group
            label="Email :"
            label-size="sm"
            label-for="input-2"
            label-cols-sm="4"
            label-align-sm="right"
            label-class="font-weight-bold my-auto px-0 pt-0"
            class="m-2"
          >
            <b-form-input
              class="m-1"
              placeholder="Votre email "
              id="input-2"
              size="sm"
              v-model="userEmail"
              :state="state"
              trim
            ></b-form-input>
          </b-form-group>
          <b-form-group
            label="Password:"
            label-size="sm"
            label-for="input-3"
            label-cols-sm="4"
            label-align-sm="right"
            label-class="font-weight-bold my-auto px-0 pt-0"
            class="m-2"
          >
            <b-form-input
              class="m-1"
              placeholder="Mot de passe"
              type="password"
              id="input-3"
              size="sm"
              v-model="userPassword"
              :state="state"
              trim
            ></b-form-input>
          </b-form-group>

          <!-- Sign In   Card  -->
        </b-form-group>
        <b-button variant="success" class="mx-auto" @click="signUp"
          >M'inscrire</b-button
        >
      </b-card>

      <b-card
        bg-variant="transparent"
        class="d-flex mx-3 p-1"
        style="height: 30vh"
      >
        <b-form-group
          label-cols-lg="3"
          label="Sign-In"
          label-size="lg"
          label-class="font-weight-bold my-auto px-0 pt-0"
          class="mb-1 mx-2"
        >
          <b-form-group
            label="Email:"
            label-size="sm"
            label-for="input-4"
            label-cols-sm="4"
            label-align-sm="right"
            label-class="font-weight-bold my-auto px-0 pt-0"
            class="m-2"
          >
            <b-form-input
              class="m-1"
              placeholder="Email "
              id="input-4"
              size="sm"
              v-model="email"
              :state="state"
              trim
            ></b-form-input>
          </b-form-group>
          <b-form-group
            label="Password:"
            label-size="sm"
            label-for="input-5"
            label-cols-sm="4"
            label-align-sm="right"
            label-class="font-weight-bold my-auto px-0 pt-0"
            class="m-2"
          >
            <b-form-input
              class="m-1"
              placeholder="Mot de passe "
              id="input-5"
              size="sm"
              type="password"
              v-model="password"
              :state="state"
              trim
            ></b-form-input>
          </b-form-group>
        </b-form-group>
        <b-button variant="success" class="mt-5 mx-auto" @click="signIn"
          >Me connecter</b-button
        >
      </b-card>
    </b-row>
  </b-container>
</template>
<style >
</style>
<script>
import bgImg from "../assets/images/troov-1920x600.jpg";
export default {
  data() {
    return {
      userName: "",
      userEmail: "",
      userPassword: "",
      email: "",
      password: "",
      bgimage: bgImg,
      loginOk: false,
    };
  },
  computed: {
    state() {
      return (
        this.userName.length >= 4 ||
        this.userEmail.length >= 4 ||
        this.userPassword.length >= 8 ||
        this.email.lentgh >= 4 ||
        this.password.length >= 8
      );
    },

    invalidFeedback() {
      if (
        this.userName.length > 0 ||
        this.userEmail.length >= 0 ||
        this.userPassword.length >= 0 ||
        this.email.length >= 0 ||
        this.password.length >= 0
      ) {
        return "Entrez au moins 4 caractères.";
      } else {
        return "Tous les champs doivent être remplis.";
      }
    },
  },
  methods: {
    async signUp() {
      //on envoie les data user au backend
      const res = await fetch(`http://localhost:3000/users/sign-up`, {
        method: "post",
        headers: {
          "Access-Control-Allow-Origin": "*",
          "Content-Type": "application/json",
        },
        body: JSON.stringify({
          userName: this.userName,
          userEmail: this.userEmail,
          userPassword: this.userPassword,
        }),
      })
        .then((res) => res.json())
        .then((res) => {
          console.log("res", res);
          // si le user a été ajouté => petit popup succès/erreur
          if (res.error[0] === "ok") {
            //alert('Vous êtes enregistré !!')
            this.$router.push("/objectScreen");
          } else {
            alert(res.error);
          }
        })
        .catch((err) => console.error(err));
    },
    async signIn() {
      //on envoie les data user au backend
      const res = await fetch(`http://localhost:3000/users/sign-in`, {
        method: "post",
        headers: {
          "Access-Control-Allow-Origin": "*",
          "Content-Type": "application/json",
        },
        body: JSON.stringify({
          userEmail: this.email,
          userPassword: this.password,
        }),
      })
        .then((res) => res.json())
        .then((res) => {
          console.log("res", res);
          // si le user a été ajouté => petit popup succès/erreur
          if (res.error[0] === "ok") {
            // alert('Vous êtes connecté !!');
            this.$router.push("/objectScreen");
          } else {
            alert(res.error);
          }
        })
        .catch((err) => console.error(err));
    },
  },
};
</script>
