<template>
  <div id="app" class="container-fluid">
    <div>
      <table class="table table-bordered">
        <thead>
          <th>#</th>
          <th>Name</th>
        </thead>
        <tbody>
          <tr v-for="e in getItems" :key="e.id">
            <td>{{ e.id }}</td>
            <td>{{ e.name }}</td>
          </tr>
        </tbody>
      </table>
      <div>
        <vuejs-paginate
          :page-count="getPaginateCount"
          :prev-text="'前へ'"
          :next-text="'後ろへ'"
          :click-handler="paginateClickCallback"
          :container-class="'pagination justify-content-center'"
          :first-last-button="true"
          :first-button-text="'最初へ'"
          :last-button-text="'最後へ'"
          :hide-prev-next="true"
          :margin-pages="0"
          :break-view-text=null
        ></vuejs-paginate>
      </div>
    </div>
  </div>
</template>

<script>
import VueJsPaginate from "vuejs-paginate";

export default {
  components: {
    "vuejs-paginate": VueJsPaginate,
  },
  props:['prevText'],
  data: function () {
    return {
      items: [],
      currentPage: 1,
      perPage: 10,
    };
  },
  created: function () {
    for (let i = 1; i <=100; i++) {
      this.items.push({
        id: i,
        name: "name_" + i,
      });
    }
  },
  computed: {
    getItems: function () {
      let start = (this.currentPage - 1) * this.perPage;
      let end = this.currentPage * this.perPage;
      return this.items.slice(start, end);
    },
    getPaginateCount: function () {
      return Math.ceil(this.items.length / this.perPage);
    },
  },
  methods: {
    paginateClickCallback: function (pageNum) {
      this.currentPage = Number(pageNum);
    },
  },
};
</script>

<style>
  @import "https://stackpath.bootstrapcdn.com/bootstrap/4.1.2/css/bootstrap.min.css";
</style>
