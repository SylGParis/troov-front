<!-- Please remove this file from your project -->
<template>
  <div :style="{backgroundImage:`url(${bgimage})`, height: '100vh'}" class="flex fill justify-center sm:items-center sm:pt-0">
    <!-- NavBarb component  -->
    <MyNavbar />
    
   
  </div>
</template>
<style >
/* .homePage {
  background-image: url("../assets/images/63508_944_Troov.png")
} */
</style>
<script>
import bgImg from "../assets/images/troov-1920x600.jpg";
export default {
  data() {
    return {
      bgimage: bgImg,
    };
  }
};
</script>
