<template>
  <div class="d-inline">
    <v-icon right @click="click" >link</v-icon>
    <v-snackbar  top dark timeout="1500"  width="auto" tag="span" color="#fef102" v-model="snackbar"> Link copied! </v-snackbar>
  </div>
</template>

<script>
export default {
name: "LinkButton",
 data:()=>({
   snackbar:false
 }),
 props:['copyLink'],
 methods: {
  click:function(){
    console.log( this.copyLink +  " clicked");
    navigator.clipboard.writeText(this.copyLink);
    this.snackbar = true;
  }
 }
}
</script>

<style scoped>
.v-snack__wrapper {
  max-width: none;
}
</style>