<template>
  <div class="d-inline">
    <v-icon right @click="click" >link</v-icon>
    <v-snackbar  top dark  text  timeout="1500"  width="auto" tag="span" color="#dddddd" v-model="snackbar"> <span  > Link copied! </span> </v-snackbar>
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
    //console.log( this.copyLink +  " clicked");
    // In order to work without https://
    // https://stackoverflow.com/questions/51805395/navigator-clipboard-is-undefined
    //
    if (navigator.clipboard && window.isSecureContext){
        navigator.clipboard.writeText(this.copyLink);
        this.snackbar =true;
    }else{
      let textArea = document.createElement("textarea");
      textArea.value = this.copyLink;
      // make the textarea out of viewport
      textArea.style.position = "fixed";
      textArea.style.left = "-999999px";
      textArea.style.top = "-999999px";
      document.body.appendChild(textArea);
      textArea.focus();
      textArea.select();
      this.snackbar = true;
      return new Promise((res, rej) => {
        // here the magic happens
        document.execCommand('copy') ? res() : rej();
        textArea.remove();

      });
    }





  }
 }
}
</script>

<style scoped>
.v-snack__wrapper {
  max-width: none;
}
</style>