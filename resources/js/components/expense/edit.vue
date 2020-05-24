    

<template>
  
  <div>

 <div class="row">
  <router-link to="/expense" class="btn btn-primary">All Expense </router-link>
   
 </div>



    <div class="row justify-content-center">
      <div class="col-xl-12 col-lg-12 col-md-12">
        <div class="card shadow-sm my-5">
          <div class="card-body p-0">
            <div class="row">
              <div class="col-lg-12">
                <div class="login-form">
                  <div class="text-center">
                    <h1 class="h4 text-gray-900 mb-4"> Expense Update</h1>
                  </div>

       <form class="user" @submit.prevent="expenseUpdate">

        <div class="form-group">

          <div class="form-row">
            <div class="col-md-12">
         <label for="exampleFormControlTextarea1"><b>Expense Details</b></label>
      <textarea class="form-control" id="exampleFormControlTextarea1" rows="3" v-model="form.details"></textarea>
  <small class="text-danger" v-if="errors.details"> {{ errors.details[0] }} </small> 
            </div> 

 <div class="col-md-12"><br>
 	<label for="exampleFormControlTextarea1"><b>Expense Amount</b></label>
         <input type="text" class="form-control" id="exampleInputFirstName" placeholder="Enter Your Amount" v-model="form.amount">
  <small class="text-danger" v-if="errors.amount"> {{ errors.amount[0] }} </small> 
            </div> 


            
          </div>
        </div>
       
         
 


        <div class="form-group">
          <button type="submit" class="btn btn-primary btn-block">Update</button>
        </div>
        
      </form>
                  <hr>
                  <div class="text-center">
  
  
                  </div>
                  <div class="text-center">
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>


</template>



<script type="text/javascript">
  
  export default {
    created(){
      if (!User.loggedIn()) {
        this.$router.push({name: '/'})
      }
    },

    data(){
    return {
      form:{
        details: '',
        amount: ''
       
        
      },
      errors:{},
    }
  },
  created(){
  	let id = this.$route.params.id
  	axios.get('/api/expense/'+id)
  	.then(({data}) => (this.form = data))
  	.catch(console.log('error'))
  },

  methods:{
    
  expenseUpdate(){
  	  let id = this.$route.params.id
       axios.patch('/api/expense/'+id,this.form)
       .then(() => {
        this.$router.push({ name: 'expense'})
        Notification.success()
       })
       .catch(error =>this.errors = error.response.data.errors)
     },
  } 


  }
   
</script>


<style type="text/css">
  
</style>