<template>
  <div class="container-fluid">
    <div class="row">
    <div class="col-md-12 col-sm-12 col-xs-12 nopadding">
      <div class="filtering">
      <h1>Filter</h1>
        <div class="form-group">
          <label for="search" class="search-label">Search</label>
          <input type="text" id="search" v-model="search" autofocus>
        </div>
          <div class="form-group">
            <label for="category">Category</label>
            <b-form-select id="category" v-model="selected_cat" :options="category" ></b-form-select>
          </div>
        <div class="form-group">
          <label for="location">Location</label>
          <b-form-select id="location" v-model="selected_loc" :options="location" ></b-form-select>
        </div>

      </div>
    </div>
    </div>
      <div class="row">

      <div class="list col-md-4 col-sm-4 col-xs-12" v-for="feed in filteredData">
          <h6>Nr: {{feed.number}} from {{feed.date}}</h6> <span class="cat">{{feed.category}}</span>
        <br>
        <h5>{{feed.title}}</h5>
        <h6>{{feed.description}}</h6>
        <h6>{{feed.location}}</h6>
          <b-button>CONTACT</b-button>
      </div>
    </div>
  </div>
</template>

<script>
  import feedData from '../feed.json';

export default {
  name: 'list',
  data() {
    return {
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
      feedData
    }
  },
  computed: {
    filteredData: function () {

      return this.feedData.data.filter(function (feed) {

        return feed.title.toUpperCase().indexOf(this.search.toUpperCase()) !== -1 && feed.category.indexOf(this.selected_cat) !== -1 && feed.location.indexOf(this.selected_loc) !== -1;
      }.bind(this));

    }
  }
}


</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>

.filtering {
  background-color: sandybrown;
  color: #fff;
  padding: 20px;
}

.nopadding {
  padding: 0 !important;
  margin: 0 !important;
}

  .list {
    margin-top: 10px;
    padding: 20px;
    background-color: antiquewhite;
    color: sandybrown;
  }

</style>
