<template>
  <div id="app">
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <div v-if="visibility">
      <ol>
        <li v-for="name in names" :key="name.id">{{name.id}} {{name.fname}} {{name.lname}}
              <button @click="deleteEvent(name.id)">Delete</button>
              <button @click="editevent(name.id)">Edit</button>
        </li>
      </ol>
    </div>
    
		<button @click="visibility = !visibility">{{visibility ? 'Hide' : 'Show'}}</button>
		<br>
		<h1>Add</h1>
		<h3>First Name</h3>
		<input v-model="fname">
		<h3>Last Name</h3>
		<input v-model="lname">
		<br>
		<button @click="input">Save</button>


		<template v-if="id_edit">
			<h1>Edit</h1>
			<h3>First Name</h3>
			<input v-model="fname">
			<h3>Last Name</h3>
			<input v-model="lname">
			<br>
			<button @click="edit(id_edit)">Edit</button>
		</template>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    
  },
  data : function() {
    return {
				fname:'',
				lname:'',
				
				names :[
					{id:1, fname : 'aa', lname : 'AA'},
					{id:2, fname : 'bb', lname : 'BB'},
					{id:3, fname : 'cc', lname : 'CC'},
					{id:4, fname : 'dd', lname : 'DD'},
					{id:5, fname : 'ee', lname : 'EE'}
				],
				visibility : true,
				id_edit : null
		};
  },
			methods : {
				input(){
					let id = this.names[this.names.length-1].id
					this.names.push({
						id : id+1,
						fname : this.fname,
						lname : this.lname
					})
					this.fname=''
					this.lname=''
				},
				edit(id){

					this.names = this.names.map(x =>
						x.id === id ? {id,fname:this.fname,lname:this.lname} : x
					)

					// let a = this.names.findIndex(x => x.id===id)
					
					// this.names.splice(  a  , 1 ,{id,fname:this.fname,lname:this.lname})
					this.id_edit = null
					this.fname = ''
					this.lname = ''
				},
				editevent(id){
					this.id_edit = id 
				},
				deleteEvent(event) {
					this.names = this.names.filter(name => name.id !== event)
				}
			}
}
</script>

<style>

</style>
