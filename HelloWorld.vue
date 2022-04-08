<template>
  <div class="xendit-form-container">
    <div class="cat-fact">
       <h1>Cat Fact</h1>
        <p> {{ catFact }} </p>
        <button class="btn btn-primary" @click="getCatFact"> Get new Cat Fact </button>
    </div>

    <h3> Xendit - mock up</h3>
    <form @submit.prevent="submitForm">
      <label path="amount" for="amount">Total Amount</label>
            <input path="amount" id="amount" v-model="amount"/>
      <br />
      <label path="currency" for="currency">Currency</label>
            <input path="currency" id="currency"  v-model="currency" readonly />
      <br />  
      <input type="submit" class="submit" value="Next" />
    </form>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data : function() {
    return {
      amount : '',
      currency : 'IDR',
      catFact: ''
    }
  },
  methods: {
    submitForm() {
      console.log(this.amount, this.currency)
      const reqPayload = {
        amount : this.amount,
        currency: this.currency
      }
      return fetch("http://localhost:8080/peace-poc/xendit2/confirm",
        {
            headers: {
            'Accept': 'application/json',
            'Content-Type': 'application/json'
            },
            method: "POST",
            body: JSON.stringify(reqPayload)
        }).then( res => res.json())
        .then( data => console.log(data))
        .catch( err => console.log(err))
    },
    async getCatFact(){
      const response = await fetch("https://catfact.ninja/fact")
      const jsonResponse = await response.json();
      this.catFact = jsonResponse.fact
     }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
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
label {
  margin-right: 5px;
}
input {
  margin: 10px 0px;
}
</style>