<template>
  <div class="container-fluid">
    <div class="col-xs-12">
      <div class="filtering">
      <h1>Filter</h1>
        <div class="form-group">
          <label for="search" class="search-label">Search</label>
          <input type="text" id="search">
        </div>
          <div class="form-group">
            <label for="category">Category</label>
            <b-form-select id="category" v-model="selected_cat" :options="category" ></b-form-select>
          </div>
        <div class="form-group">
          <label for="location">Category</label>
          <b-form-select id="location" v-model="selected_loc" :options="location" ></b-form-select>
        </div>
      </div>

      <div class="list">
        <ul>
          <li v-for="feed in feedData.data">{{feed.number}}</li>
        </ul>
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
      selected_cat: null,
      category: [
        { value: null, text: '--select--' },
        { value: 'Search', text: 'Search' },
        { value: 'Gift', text: 'Gift' }
      ],
      selected_loc: null,
      location: [
        { value: null, text: '--select--'},
        { value: 'Point A', text: 'Point A'},
        { value: 'Point B', text: 'Point B'},
        { value: 'Point C', text: 'Point C'},
        { value: 'Point D', text: 'Point D'},
        { value: 'Point E', text: 'Point E'},
      ],
      feedData
    }
  }
}

console.log(feedData.data);
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>

.filtering {
  background-color: sandybrown;
  color: #fff;
  padding: 20px;
}


</style>
