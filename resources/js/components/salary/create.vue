  

<template>
  
  <div>

 <div class="row">
  <router-link to="/employee" class="btn btn-primary">All Employee </router-link>
   
 </div>



    <div class="row justify-content-center">
      <div class="col-xl-12 col-lg-12 col-md-12">
        <div class="card shadow-sm my-5">
          <div class="card-body p-0">
            <div class="row">
              <div class="col-lg-12">
                <div class="login-form">
                  <div class="text-center">
                    <h1 class="h4 text-gray-900 mb-4">Pay Salary </h1>
                  </div>

      <form class="user" @submit.prevent="SalaryPaid">

        <div class="form-group">

          <div class="form-row">
            <div class="col-md-6">
            	<label for="exampleFormControlSelect1"><b>Name</b></label>
         <input type="text" class="form-control" id="exampleInputFirstName" placeholder="Enter Your Full Name" v-model="form.name">
       <small class="text-danger" v-if="errors.name"> {{ errors.name[0] }} </small>
            </div>


     <div class="col-md-6">
     	<label for="exampleFormControlSelect1"><b>Email</b></label>
         <input type="email" class="form-control" id="exampleInputFirstName" placeholder="Enter Your Email" v-model="form.email">
         <small class="text-danger" v-if="errors.email"> {{ errors.email[0] }} </small>
            </div>     
            
          </div>
        </div>
       
        
         <div class="form-group">

          <div class="form-row">
            <div class="col-md-6">
      <label for="exampleFormControlSelect1"><b>Months</b></label>
  
  <select class="form-control" id="exampleFormControlSelect1" v-model="form.salary_month">
     <option value="January"> January </option>
     <option value="February"> February </option>
     <option value="March"> March </option>
     <option value="April"> April </option>
     <option value="May"> May </option>
     <option value="Jun"> Jun </option>
     <option value="July"> July </option>
     <option value="August"> August </option>
     <option value="September"> September </option>
     <option value="October"> October </option>
     <option value="November"> November </option>
     <option value="December"> December </option>

                       
                      </select>   
   <small class="text-danger" v-if="errors.salary_month"> {{ errors.salary_month[0] }} </small>   
            </div>


     <div class="col-md-6">
     	<label for="exampleFormControlSelect1"><b>Salary</b></label>
         <input type="text" class="form-control" id="exampleInputFirstName" placeholder="Enter Your Sallery" v-model="form.sallery">
         <small class="text-danger" v-if="errors.sallery"> {{ errors.sallery[0] }} </small>
            </div>     
            
          </div>
        </div>

       
 

 


        <div class="form-group">
          <button type="submit" class="btn btn-primary btn-block">PayNow</button>
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
        name: '',
        email: '',
        salary_month: '',
        sallery: ''
       
      },
      errors:{}
    }
  },
  created(){
  	let id = this.$route.params.id
  	axios.get('/api/employee/'+id)
  	.then(({data}) => (this.form = data))
  	.catch(console.log('error'))
  },

  methods:{
   
  SalaryPaid(){
  	  let id = this.$route.params.id
       axios.post('/api/salary/paid/'+id,this.form)
       .then(() => {
        this.$router.push({ name: 'given-salary'})
        Notification.success()
       })
       .catch(error =>this.errors = error.response.data.errors)
     },
  } 


  }
   
</script>


<style type="text/css">
  
</style>