<template>
<div class="create-auction">
  <form v-on:submit.prevent class="createAuctionForm">
    <div class="insideForm">
        <label for="title">Title: </label>
        <div class="field">
          <input id="create-title" type="text" name="title" v-model="auction.title" />
        </div>
        <label for="description">Description: </label>
        <div class="field">
          <textarea id="create-description" type="text" name="description" v-model="auction.description" /> 
        </div>
        
        <label for="startingPrice">Starting Price: </label>
        <div class="field">
          <input id="create-startingPrice" type="text" name="startingPrice" v-model="auction.startingPrice" />
        </div>
        <label for="endDate">End Date: </label>
        <div class="field">
          <input id="create-endDate" type="datetime-local" name="endDate" v-model="auction.endDate" />
        </div>
        <label for="imagePath">Image Url: </label>
        <div class="field">
          <input type="url" id="create-image"  name="imagePath" v-model="auction.imagePath" />
        </div>
        <div class="actions">
          <button id="create-submit" type="submit" v-on:click="saveAuction()">Save Auction</button>
        </div>
    </div>
    
  </form>

</div>
</template>

<script> 
import auctionService from '../services/AuctionService';

export default {
  name: "create-auction",
  data() {
    return {
      auction: {
        title: "",
        description: "",
        startingPrice: 0,
        ownerId: this.$store.state.user.id,
        endDate: "",
        imagePath: "",
      }
    };
  },
  methods: {
    saveAuction() {
      auctionService.addAuction(this.auction).then(response => {
          if(response.status === 201) {
            this.$router.push({ name: 'home'});
          }
        
      })
    }
  }
};
</script>
<style>
.createAuctionForm{
  text-align: center;
  border-radius: 50%;
  width: 30vw;
  height: 30vw;
  background-position: center;
  background-image: url('../img/green-dollar-sign-icon-28.png');
  /* background: linear-gradient(to top right, #1abc9c, #3498db); */
  position: relative;
  color: black;
}

.insideForm {
  text-align: center;
  position: relative;
  margin: 10%;
}

#create-description {
  max-width: 15vw;
  min-width: 15vw;
  max-height: 25vw;
}
#create-title, #create-startingPrice, #create-endDate, #create-image, #create-submit{
  width: 15vw;
}
#create-submit { 
  width: 16vw;
  color: yellow;
  background-color: green;
  
}

div.field{
  padding: 10px;
  
}
form{
  justify-content: stretch;
  border-color: #344;
  border-radius: 0px;
  border-style: solid;
  background-color:  #333;
  margin-left: auto;
  margin-right: auto;
  margin-top: 10vw;
  color: white;
  padding: 15px;
  width: 20vw;
  border-width: 10px;
  border-color: brown;
}
div.logo img{
  display: flex;
  justify-content: center;
  width: 100px;
}
</style>