<template>
  <div class="modalSection " >
    <div class="flexedSection" >
    <img class="celebrantImg " :src="celebrant.img" alt="img" />
  <div class="celebrantInfo" >
    <h1> {{celebrant.firstName}} </h1>
    <span> {{celebrant.age}} </span>
  </div>
    </div>
 <span @click="deleteCelebrant " :style="{cursor: 'pointer'}" class="deleteIcon" ><Icon icon="ei:trash"  /> </span>
  </div>
</template>

<script>

import { Icon } from '@iconify/vue';

export default {
name: "Modal",
props: {
    celebrant:  Object,
    celebrants: Array,
},
components: {
  Icon
},
data() {
    return {
    
    }
    },
    methods: {
       deleteCelebrant() {
      //Since props are immutable, The parent component is only where we can mutate our array and to do this we send an Emit event with the celebrant information - So to emit, first we write out the function we're sending(Which we got from our parent component initially btw) then we write the information we want to emit
      this.$emit('delete-celebrant', this.celebrant.id);
    },
    },
}
</script>

<style scoped >
.modalSection {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 20px;
}
.flexedSection{
  display: flex;
  align-items: center;
  gap: 20px;
}
.celebrantImg{
  border-radius: 50%;
  width: 100px;
  height: 100px;
}
.celebrantInfo{
  display: flex;
  flex-direction: column;
  gap: 5px;
}
.celebrantInfo h1{
  font-size: 30px;
  font-weight: 500;
}
.celebrantInfo span{
  font-size: 20px;
}
.deleteIcon{
  cursor: pointer;
  font-size: 35px;
}

@media (max-width: 600px) {
  .celebrantImg{
    width: 50px;
    height: 50px;
  }
  .celebrantInfo h1{
    font-size: 20px;
  }
  .celebrantInfo span{
    font-size: 16px;
  }
  .deleteIcon{
    font-size: 26px;
  }
}
</style>