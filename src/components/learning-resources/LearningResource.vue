<template>
  
  <base-dialog v-if="confirmDel" title="Delete" ok="Close" @close="confirmClosure">
    <template v-slot:default>
      <p>Do you want to delete?</p>
      <p>Click confirm to delete.</p>
    </template>
    <template #actions>
      <base-button @click="confirm">Okay</base-button>
    </template>
  </base-dialog>

 <li>
  <base-card>
      <header>
        <h3>{{ title }}</h3>
        <base-button mode="flat" @click="open_dialog">Delete</base-button>
      </header>
      <p>{{ description }}</p>
      <nav>
        <a :href="link">View Resource</a>
      </nav>
   </base-card>
 </li>
</template>

<script>
export default {
  props: ['id', 'title', 'description', 'link'],
  inject: ['deleteResource'],
  data() {
    return {
      confirmDel: false,
    }
  },
  methods:{
    open_dialog(){
      this.confirmDel=true;
    },
    confirmClosure(){
      this.confirmDel=false;
    }, 
    confirm(){
      if(this.confirmDel){
        this.deleteResource(this.id);
        this.confirmDel=false;
      }      
    }
  }
};
</script>

<style scoped>
li {
  margin: auto;
  max-width: 40rem;
}

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

h3 {
  font-size: 1.25rem;
  margin: 0.5rem 0;
}

p {
  margin: 0.5rem 0;
}

a {
  text-decoration: none;
  color: #ce5c00;
}

a:hover,
a:active {
  color: #c89300;
}
</style>