<template>
  <div class="container">
    <div class="row">
      <div class="col-md-12">
        <div class="card">
          <div v-if="errors.length" class="card-header">
            <h3 class="text-danger">Please fill the requireds fields</h3>
            <ul>
              <li v-for="error in errors" :key="error">{{ error }}</li>
            </ul>
          </div>
          <div v-else></div>

          <div class="card-body">
            <form @submit="validateForm">
              <div class="form-group">
                <label for="exampleFormControlInput1">Name</label>
                <input
                  type="text"
                  v-model="name"
                  class="form-control"
                  id="exampleFormControlInput1"
                  placeholder="Roberto"
                />
              </div>
              <div class="form-group">
                <label for="exampleFormControlInput2">Image URL:</label>
                <input
                  type="text"
                  v-model="img"
                  class="form-control"
                  id="exampleFormControlInput2"
                  placeholder="https://ali.cdn.com/image.png"
                />
              </div>
              <div class="form-group">
                <label class="sr-only" for="inlineFormInputGroup">Price:</label>
                <div class="input-group mb-2">
                  <div class="input-group-prepend">
                    <div class="input-group-text">$</div>
                  </div>
                  <input
                    type="number"
                    v-model="price"
                    inputmode="numeric"
                    step="0.01"
                    class="form-control"
                    id="exampleFormControlInput3"
                    placeholder="3"
                  />
                </div>
              </div>
              <div class="form-group">
                <label for="exampleFormControlTextarea1">Description</label>
                <textarea
                  class="form-control"
                  v-model="description"
                  id="exampleFormControlTextarea1"
                  rows="3"
                  placeholder="A bunch of carrots a nice item"
                ></textarea>
              </div>
              <div class="form-group">
                <label for="exampleFormControlSelect1">Type</label>
                <select
                  v-model="type"
                  class="form-control"
                  id="exampleFormControlSelect1"
                >
                  <option disabled value="">
                    Please select one type of item
                  </option>
                  <option>Vegetable</option>
                  <option>Fruit</option>
                  <option>Sweet</option>
                  <option>Dairy</option>
                  <option>Drink</option>
                </select>
              </div>
              <button
                type="submit"
                @click="addItem()"
                class="btn btn-primary my-3 w-100"
              >
                Submit
              </button>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "RegisterObjects",
  data() {
    return {
      items: [],
      name: "",
      img: "",
      price: "",
      description: "",
      type: "",
      errors: [],
    };
  },
  methods: {
    async addItem() {
      const response = await axios.post("http://localhost:3000/items", {
        name: this.name,
        img: this.img,
        price: this.price,
        description: this.description,
        type: this.type,
        created_at: new Date(),
      });
      this.items = [...this.items, response.data];
      this.name = "";
      this.img = "";
      this.price = "";
      this.description = "";
      this.type = "";
    },
    validateForm: function (e) {
      if (
        this.name &&
        this.img &&
        this.price &&
        this.description &&
        this.type
      ) {
        return true;
      }
      if (!this.name) {
        this.errors.push("Name is required");
      }
      if (!this.img) {
        this.errors.push("Image URL is required");
      }
      if (!this.price) {
        this.errors.push("Price is required");
      }
      if (!this.description) {
        this.errors.push("Description is required");
      }
      if (!this.type) {
        this.errors.push("Type is required");
      }
      e.preventDefault();
    },
  },
};
</script>
