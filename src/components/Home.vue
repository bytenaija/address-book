<template>
<div>
<b-navbar toggleable="md" type="dark" variant="info">

  <b-navbar-toggle target="nav_collapse"></b-navbar-toggle>

  <b-navbar-brand href="#">Take a Climb</b-navbar-brand>

  <b-collapse is-nav id="nav_collapse">

    <b-navbar-nav>
      <b-nav-item href="#"  @click="add=true; edit=false; contact={}; showModal=true">Add Contact</b-nav-item>
      <b-nav-item href="#"  @click="deleteContact()">Delete all Contacts</b-nav-item>
    </b-navbar-nav>

    

  </b-collapse>
</b-navbar>
<div class="address-book text-center">
<button class="btn btn-primary col-md-3" @click="add=true; edit=false; contact={}; showModal=true">Add Contact</button><button class="btn btn-danger col-md-3" @click="deleteContact()">Delete All Contacts</button>
<h2> Click on each contact to view their details</h2>
  <div class="address">
   <div v-for="(contact, index) of contacts" :key="index">
   <div class="card">
  <div class="card-header" :id="'person' + index">
  {{contact.firstname}} {{contact.lastname}}
  <div class="float-right">
  <button @click="editContact(index); showModal=true">Edit</button>
   <button @click="deleteContact(index)">Delete</button>
  </div>
  </div>
  <div :class="'person' + index + ' card-body grp person'">
      <p>Gender : {{contact.gender}}</p>
      <p>Address : {{contact.address}}</p>
      <p>Company : {{contact.company}}</p>
      <p>Designation : {{contact.designation}}</p>
      <p>Department : {{contact.department}}</p>
      <p>Mobile : {{contact.mobile}}</p>
      <p>Email : {{contact.email}}</p>
  </div>
  </div>
</div>
 
  </div>
<b-modal v-model="showModal" @ok="addContact()" @cancel="contact={}">
  <div class="addEdit">
    <div class="form-group">
      <label>Firstname</label>
      <input type="text" class="form-control" v-model="contact.firstname">
    </div>
    
    <div class="form-group">
      <label>Lastname</label>
      <input type="text" class="form-control" v-model="contact.lastname">
    </div>

    <div class="form-group">
      <label>Address</label>
      <textarea type="text" class="form-control" v-model="contact.address"></textarea>
    </div>

    <div class="form-group">
      <label>Email</label>
      <input type="text" class="form-control" v-model="contact.email">
    </div>

    <div class="form-group">
      <label>Company</label>
      <input type="text" class="form-control" v-model="contact.company">
    </div>

    <div class="form-group">
      <label>Department</label>
      <input type="text" class="form-control" v-model="contact.department">
    </div>


    <div class="form-group">
      <label>Gender</label>
       <select type="text" class="form-control" v-model="contact.gender">
      <option value="Male">Male </option>
      <option value="Female">Female </option>
      </select>
    </div>
    
     <div class="form-group">
      <label>Mobile Phone</label>
      <input type="text" class="form-control" v-model="contact.mobile">
    </div>

     <div class="form-group">
      <label>Designation</label>
       <input type="text" class="form-control" v-model="contact.designation">
    </div>
    
    
    
   
    
    
   
  </div>
  </b-modal>
</div>
  </div>
</template>

<script>
import jquery from "jquery";
window.$ = global.$ = jquery;

$(document).ready(function(){
  $(".address").click(function(e){
    var cls = e.target.id;
    
    if($("." + cls).hasClass("anim")){
  $("." + cls).removeClass("anim");
  $("." + cls).addClass("grp");
    }else{
      $('.person').addClass('grp')
      $('.person').removeClass("anim");
      $("." + cls).removeClass("grp");
      
    $("." + cls).addClass("anim");
    }
  })
});
export default {
  name: 'Home',
  data: function(){
    return({
    index : '',
    add : false,
    showModal : false,
    edit : false,
		contact: { firsName :'', lastName : '', company : '', address : '', mobile : '', email : '', department : '', designation : ''},
		contacts: [
			{
				id: 1,
				lastname: 'Smith',
				firstname: 'John',
				gender: 'Male',
        company : 'Andela',
        address : 'Festac Road, Lagos',
        mobile : '08076483773',
        email : 'byte@andela.com',
        department :'R&D',
        designation: 'Chief Discovery Officer'
        
			},
			{
				id: 2,
				lastname: 'Smith',
				firstname: 'Mary',
				gender: 'Female',
        company : 'Flutterwave',
        address : '95 Festac Road, Lagos',
        mobile : '08076474664',
        email : 'mary.smith@flutterwave.com',
        department :'R&D',
        designation: 'Software Developer'
			},

      {
				id: 3,
				lastname: 'Smith',
				firstname: 'Grace',
				gender: 'Female',
        company : 'Paystack',
        address : '201 Ikoyi Road, Lagos',
        mobile : '08076474664',
        email : 'grace.smith@paystack.com',
        department :'Finance',
        designation: 'CFO'
			}
	
		]
    }
    )
	},



	// Methods we want to use in our application are registered here
	methods: {
		// Adds a contact to the existing contacts array
		addContact: function() {
      if(this.edit){
        this.contacts[this.index] = this.contact;
        this.contact = { firsName :'', lastName : '', company : '', address : '', mobile : '', email : '', department : '', designation : ''};
      }else{
        if (this.contact.firstname) {
          this.contact.id = this.contacts.length;
          this.contacts.push(this.contact);
          console.log(this.contacts)
          this.contact = { firsName :'', lastName : '', company : '', address : '', mobile : '', email : '', department : '', designation : ''};
        }
      }
		},
    editContact: function(index){
      this.edit = true;
      this.index = index;
      this.contact = this.contacts[index];
      console.log(this.contact);
    },
		deleteContact: function(index) {
      console.log(index);
      if(index !== undefined){
        	if (confirm("Are you sure you want to delete this contact?")) {
				this.contacts.splice(index, 1);
			}

      }else{
        if (confirm("Are you sure you want to delete all contacts?")) {
				this.contacts = [];
			}
      }
		
		}
	}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.row{
  margin-top: 3rem;
}
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.grp{
  position:relative;
  bottom:50%;
  display: none;
}

.anim{
animation : reveal;
animation-delay: 0s;
animation-duration:7s;
animation-fill-mode: forwards;
animation-timing-function:ease-in-out;
}

@keyframes reveal {
  0%{
    display:none;
    bottom: 50%
  } 

  10%{
    display:none;
    bottom: 40%
  }
  25%{
    display:block;
    bottom: 30%
  }

  100%{
    display:block;
    bottom: 0%;
  }
}

  .address{
    display:grid;
    grid-template-columns: 1fr;
    grid-gap:1rem;
    
  }

  .address-book{
    width: 70%;
    margin: 2rem auto;
  }

.btn{
  margin: 2rem;
}

.card-body{
  text-align: left;
  z-index: 200;
}

.card-header{
  cursor: pointer;
}

.addEdit{
  text-align: left;
}

@media only screen and (min-width: 750px) {
.row{
  margin-top: 3rem;
}
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.grp{
  position:relative;
  bottom:50%;
  display: none;
}

.anim{
animation : reveal;
animation-delay: 0s;
animation-duration:7s;
animation-fill-mode: forwards;
animation-timing-function:ease-in-out;
}

@keyframes reveal {
  0%{
    display:none;
    bottom: 50%
  } 

  10%{
    display:none;
    bottom: 40%
  }
  25%{
    display:block;
    bottom: 30%
  }

  100%{
    display:block;
    bottom: 0%;
  }
}

  .address{
    display:grid;
    grid-template-columns: repeat(3, 400px);
    grid-gap:1rem;
    
  }

  .address-book{
    width: 80%;
    margin: 5rem auto;
  }

.btn{
  margin: 2rem;
}

.card-body{
  text-align: left;
  z-index: 200;
}

.card{
  z-index: 200;
}

.card-header{
  cursor: pointer;
}

.addEdit{
  text-align: left;
}
}
  

</style>
