<template>
  <div id="app">
    <div class="wrapper">
      <header class="wrapper__header">
        <Select :department="department" @changeDepartment="changeDepartment" />
        <Search @changeSearch="changeSearch" :search="search" />
      </header>
      <section class="wrapper__cards" v-if="filteredData.length != 0">
        <Card v-for="item in filteredData" :key="item.name" :item="item" />
      </section>
      <div v-else class="wrapper__no-records">
        <p>No records to show</p>
      </div>
      <footer class="wrapper__footer">
        <Pagination
          @changePage="changePage"
          :initialPage="currentPage"
          :perPage="perPage"
          :totalPage="totalPage"
        />
      </footer>
    </div>
  </div>
</template>

<script>
import Pagination from "@/components/Pagination";
import Select from "@/components/Select";
import Search from "@/components/Search";
import Card from "@/components/Card";
export default {
  name: "App",
  components: {
    Pagination,
    Select,
    Search,
    Card,
  },
  data() {
    return {
      currentPage: 1,
      perPage: 6,
      totalPage: 0,
      search: "",
      selected: "",
      filter: [],
      data: [
        {
          name: "Bret",
          email: "bret@gmail.com",
          phone: "1580 1308926",
          department: "Software",
        },
        {
          name: "Antonette",
          email: "antonette@gmail.com",
          phone: "1580 1308926",
          department: "Customer Service",
        },
        {
          name: "Samantha",
          email: "samantha@gmail.com",
          phone: "1580 1308926",
          department: "Software",
        },
        {
          name: "Karianne",
          email: "karianne@gmail.com",
          phone: "1580 1308926",
          department: "Customer Service",
        },
        {
          name: "Kamren",
          email: "kamren@gmail.com",
          phone: "1580 1308926",
          department: "Human Resources",
        },
        {
          name: "Dennis",
          email: "dennis@gmail.com",
          phone: "1580 1308926",
          department: "Human Resources",
        },
        {
          name: "Kurtis",
          email: "kurtis@gmail.com",
          phone: "1580 1308926",
          department: "Human Resources",
        },
        {
          name: "Nicholas",
          email: "nicholas@gmail.com",
          phone: "1580 1308926",
          department: "Human Resources",
        },
        {
          name: "Glenna",
          email: "glenna@gmail.com",
          phone: "1580 1308926",
          department: "Software",
        },
        {
          name: "Clementina",
          email: "clementina@gmail.com",
          phone: "1580 1308926",
          department: "Customer Service",
        },
        {
          name: "Brad",
          email: "brad@gmail.com",
          phone: "1580 1308926",
          department: "Software",
        },
        {
          name: "Krasimir",
          email: "krasimir@gmail.com",
          phone: "1580 1308926",
          department: "Human Resources",
        },
        {
          name: "Mark",
          email: "mark@gmail.com",
          phone: "1580 1308926",
          department: "Software",
        },
        {
          name: "Kia",
          email: "kia@gmail.com",
          phone: "1580 1308926",
          department: "Software",
        },
        {
          name: "Josh",
          email: "josh@gmail.com",
          phone: "1580 1308926",
          department: "Customer Service",
        },
        {
          name: "Rasmus",
          email: "rasmus@gmail.com",
          phone: "1580 1308926",
          department: "Human Resources",
        },
        {
          name: "Jim",
          email: "jim@gmail.com",
          phone: "1580 1308926",
          department: "Software",
        },
        {
          name: "Ankur",
          email: "ankur@gmail.com",
          phone: "1580 1308926",
          department: "Software",
        },
        {
          name: "Simon",
          email: "simon@gmail.com",
          phone: "1580 1308926",
          department: "Human Resources",
        },
        {
          name: "Evan",
          email: "evan@gmail.com",
          phone: "1580 1308926",
          department: "Customer Service",
        },
        {
          name: "Kass",
          email: "kass@gmail.com",
          phone: "1580 1308926",
          department: "Customer Service",
        },
        {
          name: "George",
          email: "george@gmail.com",
          phone: "1580 1308926",
          department: "Software",
        },
        {
          name: "Michelle",
          email: "michelle@gmail.com",
          phone: "1580 1308926",
          department: "Software",
        },
      ],
    };
  },
  created() {
    this.totalPageCount(this.data);
  },
  computed: {
    department() {
      let data = [
        ...new Map(
          this.data.map((x) => [x["department"], x.department])
        ).values(),
      ];
      data.push("Full Data");
      return data;
    },
    filteredData: {
      get: function() {
        let data = [];
        if (this.currentPage == 1 && this.search == "") {
          data = this.data.slice(0, this.perPage);
          this.totalPageCount(this.data);
        }
        if (this.filter.length != 0) {
          data = this.filter.slice(
            this.perPage * this.currentPage - this.perPage,
            this.perPage * this.currentPage
          );
          this.totalPageCount(this.filter);
        } else if (this.search != "" && this.filter.length == 0) {
          data = [];
        } else {
          data = this.data.slice(
            this.perPage * this.currentPage - this.perPage,
            this.perPage * this.currentPage
          );
        }
        return data;
      },
      set: function(value) {
        this.filter = value;
      },
    },
  },
  methods: {
    changePage(page) {
      this.currentPage = page;
    },
    changeDepartment(department) {
      this.selected = department;
      this.currentPage = 1;
      if (this.selected == "Full Data") {
        this.search = "";
        this.filteredData = this.data;
      }
      if (this.search != "")
        this.filteredData = this.data.filter(
          (x) =>
            x.department == this.selected &&
            x.name.toUpperCase().includes(this.search.toUpperCase())
        );
      else
        this.filteredData = this.data.filter(
          (x) => x.department == this.selected
        );
    },
    totalPageCount(data) {
      this.totalPage = Math.ceil(data.length / this.perPage);
    },
    changeSearch(search) {
      this.search = search;
      this.currentPage = 1;
      let department = this.department.filter((x) => x == this.selected)[0];
      let filter = [];
      if (department != undefined && department != "Full Data") {
        filter = this.data.filter(
          (x) =>
            x.name.toUpperCase().includes(search.toUpperCase()) &&
            x.department == department
        );
      } else {
        filter = this.data.filter((x) =>
          x.name.toUpperCase().includes(search.toUpperCase())
        );
      }
      if (filter.length != 0) this.totalPageCount(filter);
      else this.totalPageCount([{}]);

      this.filteredData = filter;
    },
  },
};
</script>

<style scoped></style>
