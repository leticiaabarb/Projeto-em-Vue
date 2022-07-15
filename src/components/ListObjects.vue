<template>
  <div class="container main">
      <h1>Shopping List</h1>
      <button class="btn btn-primary mb-5" @click="created()">Refresh List</button>
      <button class="btn-add btn btn-success mb-5" @click="this.$router.push({name: 'register'})">Add to List</button>
      <div v-if="items.length > 0" class="card shadow-lg bg-white-rounded">
        <ul class="list-group list-group-flush">
          <li class="list-group-item" v-for="item in items" :key="item.id">
              <img :src="item.img" class="card-img-top w-25" alt="...">
              <div class="card-body">
                <h2 class="card-title">{{ item.name }}</h2>
                <h5 class="card-text">{{ item.description }}</h5>
              </div>
              <p><strong>Id: </strong> <span>{{ item.id }}</span></p>
              <p><strong>Price: </strong> <span>{{ item.price }}</span></p>
              <p><strong>Created at: </strong> <span>{{ item.created_at }}</span></p>
              <p><strong>Type: </strong> <span>{{ item.type }}</span></p>
              <div class="card-body">
                <button class="btn btn-danger ml-3" @click="removeItem(item)">Remove</button>
              </div>
          </li>
        </ul>
      </div>
      <div v-else>
        <h1>No items found</h1>
      </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "ListObjects",
  data() {
    return {
      items:[],
    };
  },
  methods: {
    async created(){
      const response = await axios.get("http://localhost:3000/items");
      this.items = response.data;
    },
  },
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
.btn-add {
  margin-left:1rem;
}

</style>
