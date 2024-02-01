<script>
import ModalVue from './components/modal/Modal.vue'

export default {
  name: "App",
  components: {
    ModalVue,
  },
  data() {
    return {
       celebrants: [
           {
    id: 1,
    img: './personOne.jpg' ,
    firstName: "Bernie Yates",
    age: "29 years" 
  },
  {
    id: 2,
    img: './personTwo.jpg',
    firstName: "Hester Hogan",
    age: "32 years"
  },
  {
    id: 3,
    img:'./personThree.jpg',
    firstName: "Elene Bates",
    age: "36 years"
  },
  {
    id: 4,
    img: './personTwo.jpg',
    firstName: "Sean Walsh",
    age: "34 years"
  },
  {
    id: 5,
    img: './personOne.jpg',
    firstName: "Lola Gardner",
    age: "29 years"
  },
  ],
      readMoreText: `The intention of this project is to test my vue knowlege of Creating, Reading and deleting birthdays, While the text is simply for me to do a Read more functionality as a bonus practice Rick Steves' Best of Ireland tour kicks off with the best of Dublin, followed by Ireland's must-see historical sites, charming towns, music-filled pubs, and seaside getaways — including Kinsale, the Dingle Peninsula, the Cliffs of Moher, the Aran Islands, Galway, Connemara, Giant's Causeway, and the compelling city of Belfast. All along the way, Rick's guides will share their stories to draw you in to the Emerald Isle, and the friendliness of the people will surely steal your heart. Join us for the Best of Ireland in 14 Days!`,
      slicedValue: 300,
      }
  },
  methods: {
    clearAll() {
      this.celebrants = []
    },

    AddCelebrant() {
      //Defined the object you want to add to the array
      const added = {
        id: this.celebrants.length + 1,
        img: './personOne.jpg' ,
        firstName: "Falomo Mayowa",
        age: "24 years"
      }

      //Then add the object to the array by adding the object to the spread array so it's adds to the top
      this.celebrants = [added, ...this.celebrants]

      // *or you write this but it adds to the end of the list instead
      // this.celebrants.push({
      //   id: this.celebrants.length + 1,
      //   img: './personOne.jpg' ,
      //   firstName: "Ifechukwu Okochi",
      //   age: "22 years" 
      // })
    },

    //Using the pop method would simply remove the last item in the array
    deleteLastCelebrant() {
      this.celebrants.pop()
    },

    //This function would delete any item clicked on, so we'll need to pass it as a prop to the child component then emit whatever id we clicked on back to the parent since props are immutable so we cannot run any update or delete action in thw child
     handleDeleteCelebrant(id) {
      //Now i can filter the celebrants array, update the state, or perform any other action here
      //So we then say, the old array = the filtered id array and the state is updated 
      this.celebrants = this.celebrants.filter((celebrant) => celebrant.id !== id);
    },
    handleReadMore() {
      this.slicedValue = this.readMoreText.length
    },
    handleReadLess() {
      this.slicedValue = 200
    }
  }
}
</script>

<template>
 <div class="appWrapper" >
  <div class="modalContainer" >
    <h1> {{celebrants.length}} Birthdays Today </h1> 

    <div class="container " >

    <div  v-for="celebrant in celebrants" class="mappedCelebrant" :key="celebrant.id " >
      <ModalVue :celebrants="celebrants" :celebrant="celebrant"  @delete-celebrant="handleDeleteCelebrant" />
    </div>
          <button @click="clearAll" class="clearBtn" > Clear All </button>
          <button @click="AddCelebrant" class="addBtn" > Add Celebrant </button>
          <button @click="deleteLastCelebrant" class="deleteBtn" > Delete a Celebrant </button>
    </div>
  </div>
  <div class="readMore" >
    <p>{{readMoreText.slice(0, slicedValue )}}...
      <span v-if="slicedValue == 200 "  @click="handleReadMore" :style="{cursor: 'pointer'}" >Read More </span> 
      <span v-else @click="slicedValue = 200" :style="{cursor: 'pointer'}" >Show Less </span>
       
      </p>
  </div>
 </div>
 
</template>

<style scoped>
.appWrapper{
  height: 100vh;
  width: 100vw;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
 gap: 20px;
  margin: 0 auto;
  background-color: #FAE8FF;
}
.modalContainer{
  height: fit-content;
  max-height: 100%;
  width: 700px;
  max-width: 80%;
  min-width: 350px;
  padding: 20px;
  background-color: white;
  border-radius: 20px;
box-shadow: rgba(50, 50, 93, 0.25) 0px 2px 5px -1px, rgba(0, 0, 0, 0.3) 0px 1px 3px -1px;
}
.modalContainer h1{
  width: 90%;
  font-size: 35px;
  font-weight: 400;
  margin: 0 auto;
}
.container{
  display: flex;
  flex-direction: column;
  gap: 20px;
  margin: 40px auto;
  width: 90%;
}
.clearBtn{
  width: 100%;
  padding: 10px;
  border-radius: 7px;
  background-color: #ed455e;
  color: white;
  font-size: 18px;
  border: none;
  outline: none;
  cursor: pointer;
  margin-top: 5px;
}
.addBtn{
  width: 100%;
  padding: 10px;
  border-radius: 7px;
  background-color: #146145da;
  color: white;
  font-size: 18px;
  border: none;
  outline: none;
  cursor: pointer;
  margin-top: 5px;
}
.deleteBtn{
  width: 100%;
  padding: 10px;
  border-radius: 7px;
  background-color: #5645edad;
  color: white;
  font-size: 18px;
  border: none;
  outline: none;
  cursor: pointer;
  margin-top: 5px;
}
.readMore{
  background-color: #FAE8FF;
  width: 90%;
  margin: 0 auto;
}
.readMore p{
  font-size: 22px;
}

@media (max-width: 500px) {
  .modalContainer h1{
    font-size: 22px;
  }
}
</style>
