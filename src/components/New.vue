<template>
  <div class="container-fluid">
    <div class="row">
      <div class="col-xs-12 col-sm-12 col-md-12">
        <form class="form-create" v-on:submit.prevent="addFeed()">
          <div class="form-group">
          <label>Title</label>
          <input type="text" class="form-control" v-model="feed.title" required>
          </div>
          <div class="form-group">
          <label>Description</label>
          <input type="text" class="form-control" v-model="feed.desc" required>
          </div>
          <div class="form-group">
          <label>Phone</label>
          <input type="tel" class="form-control" v-model="feed.phone" required>
          </div>
          <div class="form-group">
          <label>Category</label>
          <select name="cat" id="cat" class="form-control" v-model="feed.category" required>
            <option v-for="option in category" :value="option.value">{{option.text}}</option>
          </select>
          </div>
          <div class="form-group">
          <label>Location</label>
          <select name="loc" id="loc" class="form-control" v-model="feed.location" required>
            <option v-for="option in location" :value="option.value">{{option.text}}</option>
          </select>
          </div>
          <div class="form-group">
          <label>First Name</label>
          <input type="text" class="form-control" v-model="feed.firstname" required>
          </div>
          <div class="form-group">
          <label>Last Name</label>
          <input type="text" class="form-control" v-model="feed.lastname" required>
          </div>
          <div class="form-group">
          <label>Email</label>
          <input type="email" class="form-control" v-model="feed.email" required>
          </div>
          <div class="form-group">
          <label>Password</label>
          <input type="password" class="form-control" v-model="feed.password" required>
          </div>
          <div class="form-group">
          <div class="form-check">
            <label class="form-check-label">
              <input class="form-check-input" type="checkbox" v-model="checked">
                Agree
            </label>
          </div>
          </div>
          <button type="submit" v-bind:disabled="!checked" class="btn btn-submit">SUBMIT</button>
        </form>
      </div>
    </div>
  </div>

</template>

<script>
export default {
  name: 'new',
  data () {
    return {
      feed: {
        title: '',
        desc: '',
        phone: '',
        category: '',
        location: '',
        firstname: '',
        lastname: '',
        email: '',
        password: ''
      },
      category: [
        { value: '', text: '--select--' },
        { value: 'Search', text: 'Search' },
        { value: 'Gift', text: 'Gift' }
      ],
      location: [
        { value: '', text: '--select--'},
        { value: 'Point A', text: 'Point A'},
        { value: 'Point B', text: 'Point B'},
        { value: 'Point C', text: 'Point C'},
        { value: 'Point D', text: 'Point D'},
        { value: 'Point E', text: 'Point E'},
      ],
      checked: false,
    }
  },
  methods: {
    addFeed: function () {
      this.$http.post('http://localhost/create', {
        data: this.feed
      }).then(function (data) {
        console.log(data)
      });

    }
  }
}
</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
  .form-create {
    padding: 20px;
    background-color: #3b3936;
    float: left;
    width: 100%;

  }

  label {
    color: #ccc;
    font-size: 10px;
    margin-bottom: 0;
  }

  .form-control {
    background-color: transparent;
    border: none;
    border-radius: 0;
    border-bottom: 1px solid #ccc;
    color: #fff;
  }

  .form-control:focus {
    background-color: transparent;
    border-bottom: 1px solid #fff;
    color: #fff;
  }

  option {
    color: #000
  }

  .form-check-label {
    font-size: 16px;
  }

  .btn-submit {
    background-color: #fc7e00;
    color: #fff;
    float: right;
  }

</style>
