<template>
  <div class="container">
    <div>
      <h1>Items</h1>

      <table class="table table-hover">
        <thead>
          <tr>
            <td>ID</td>
            <td>Item Title</td>
            <td>Item Price</td>
            <td>Actions</td>
          </tr>
        </thead>

        <tbody>
          <tr v-for="item in items" :key="item.id">
            <td>{{ item.id }}</td>
            <td>{{ item.title }}</td>
            <td>{{ item.item_price }}</td>
            <td>
              <router-link
                :to="{ name: 'edit_item-id', params: { id: item.id } }"
                class="btn btn-primary"
                >Edit</router-link
              >
            </td>
            <td>
              <button class="btn btn-danger" v-on:click="deleteItem(item.id)">
                Delete
              </button>
            </td>
          </tr>
        </tbody>
      </table>
      <div class="col-lg-1">
        <a href="/">
          <b-button class="mb-3" variant="danger" type="submit">Home</b-button>
        </a>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  data() {
    return {
      items: []
    };
  },
  //Async Method
  asyncData({ params }) {
    return axios
      .get(`http://localhost/demo/api/demo/Content/data/`)
      .then(res => {
        return { items: res.data };
      });
  },
  //Mounted Method
  //   mounted() {
  //     axios.get("http://localhost/demo/api/demo/Content/data/").then(response => {
  //       this.items = response.data;
  //       console.log(this.items);
  //     });
  //   }
  //   mounted: function() {
  //     this.fetchItems();
  //   },

  methods: {
    // fetchItems() {
    //   axios
    //     .get("http://localhost/demo/api/demo/Content/data/")
    //     .then(response => {
    //       this.items = response.data;
    //       console.log(this.items);
    //     });
    // },
    deleteItem(id) {
      axios
        .post("http://localhost/demo/api/demo/Delete_item_by_id/data/" + id)
        .then(result => {
          console.log(result.data);
        });
      this.items.splice(id, this.$route.params.id);
      window.location.href = "/view_item";
    }
  }
};
</script>
