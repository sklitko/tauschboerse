<template id="modal-template">
  <div class="container-fluid">
    <div class="row">
    <div class="col-md-12 col-sm-12 col-12">
      <div class="filtering">
      <h1>Filter</h1>
        <div class="form-group">
          <label>Search</label>
          <input type="text" id="search" class="search" v-model="search" autofocus placeholder="Search text...">
        </div>
          <div class="form-group">
            <label>Category</label>
            <select name="selected_cat" id="category" class="select" v-model="selected_cat">
              <option v-for="option in category" :value="option.value">{{option.text}}</option>
            </select>
          </div>
        <div class="form-group">
          <label>Location</label>
          <select name="location" id="location" class="select" v-model="selected_loc">
            <option v-for="option in location" :value="option.value">{{option.text}}</option>
          </select>
        </div>
        <button type="button" class="btn btn-warning btn-filter float-right" v-on:click="filtered" >APPLY FILTER</button>
      </div>
    </div>
    </div>
      <div class="row">

      <div class="col-md-3 col-sm-6 col-12" v-for="feed in filteredData">
        <div class="list">
          <div class="list_head">
            <p class="list_title">Nr.{{feed.number}} from {{feed.date}}</p> <span class="cat">{{feed.category}}</span>
          </div>
          <div class="list_body">
            <p class="list_body_title">{{feed.title}}</p>
            <p class="list_body_desc">{{feed.description}}</p>
            <p class="list_body_loc"><i class="fa fa-map-marker"></i><strong> Location: {{feed.location}}</strong></p>
          </div>
           <div class="list_actions">
             <button type="button" class="btn btn-link btn-contact" @click="openModal()">CONTACT</button>
          </div>
        </div>
      </div>
    </div>
    <modal v-if="showModal">
          <h3 slot="header" class="modal-title">
            Modal title
          </h3>
          <div slot="body">
            <div class="form-group">
              <label>Name</label>
              <input type="text" class="form-control" v-model="contact.name" required>
            </div>
            <div class="form-group">
              <label>Email</label>
              <input type="email" class="form-control" v-model="contact.email" required>
            </div>
            <div class="form-group">
              <label>Description</label>
              <textarea class="form-control" v-model="contact.description" required></textarea>
            </div>
          </div>
          <div slot="footer">
            <button type="button" class="btn btn-outline-info" @click="closeModal()"> Close </button>
            <button type="button" class="btn btn-primary" data-dismiss="modal" @click="submitAndClose()">
              SEND
            </button>
          </div>
    </modal>
  </div>
</template>



<script>
  import feedData from '../feed.json';
  import Modal from './Modal'

export default {
  name: 'list',
  data() {
    return {
      contact: {
        name: '',
        email: '',
        description: ''
      },
      search: '',
      selected_cat: '',
      category: [
        { value: '', text: '--select--' },
        { value: 'Search', text: 'Search' },
        { value: 'Gift', text: 'Gift' }
      ],
      selected_loc: '',
      location: [
        { value: '', text: '--select--'},
        { value: 'Point A', text: 'Point A'},
        { value: 'Point B', text: 'Point B'},
        { value: 'Point C', text: 'Point C'},
        { value: 'Point D', text: 'Point D'},
        { value: 'Point E', text: 'Point E'},
      ],
      feedData,
      search_text: '',
      selected_category: '',
      selected_location: '',
      showModal: false
    }
  },
  computed: {
    filteredData: function () {
      return this.feedData.data.filter(function (feed) {
        return feed.title.toUpperCase().indexOf(this.search_text.toUpperCase()) !== -1 && feed.category.indexOf(this.selected_category) !== -1 && feed.location.indexOf(this.selected_location) !== -1;
      }.bind(this));

    }
  },
  methods: {
    filtered: function () {
      this.search_text = this.search;
      this.selected_category = this.selected_cat;
      this.selected_location = this.selected_loc;
    },
    openModal() {
      this.showModal = true;
    },
    closeModal() {
      this.showModal = false;
    },
    submitAndClose() {
      this.showModal = false;
      this.$http.post('http://localhost/contact', {
        data: this.contact
      }).then(function (data) {
        console.log(data)
      });
    }
  },
  components: {
    Modal
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>

.filtering {
  background-color: #3b3936;
  color: #fff;
  padding: 20px;
  float: left;
  width: 100%;
}

label {
  width: 100%;
  font-size: 10px;
  color: grey;
  margin-bottom: 0;
}

.search {
  width: 100%;
  background-color: transparent;
  border: none;
  border-bottom: 1px solid #ccc;
  outline: 0;
  color: #fff;
}



.select {
  width: 100%;
  background-color: transparent;
  border: none;
  border-radius: 0;
  border-bottom: 1px solid #ccc;
  color: #fff;
  padding: 5px 0;
  position: relative;
  outline: 0;
}

.select option {
  color: #000;
  border: none;
}

.btn-filter {
  background-color: #fc7e00;
  border: none;
  border-radius: 2px;

}

.list {
   margin-top: 15px;
    padding: 20px;
    background-color: #f2ede6;
    color: #706b66;
    float: left;
}


  .list_head, .list_body, .list_actions {
    width: 100%;
    float: left;
  }

.list_title {
  float: left;
}

.cat {
  float: right;
  background-color: #3b3936;
  color: #fff;
  padding: 1px 5px;
  font-size: 12px;
  border-radius: 2px;
}

  .list_body {
    margin-top: 20px;
  }

.list_body_desc {
  margin-bottom: 0;
}

.btn-contact, .btn-contact:hover  {
  color: #fc7e00;
  border-top: 2px solid #fc7e00;
  padding-left: 0;
  text-decoration: none;
}

</style>
