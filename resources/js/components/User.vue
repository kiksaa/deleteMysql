<template>
  <div>
    <div class="container">
      <h2 class="text-center">แสดงข้อมูล</h2>
      <table class="table table-bordered">
        <tr>
          <th>รหัส</th>
          <th>ชื่อ</th>
          <th>สกุล</th>
          <th>อายุ</th>
          <th>ลบ</th>
        </tr>
        <tr v-for="(user,index) in users">
          <td>{{user.id}}</td>
          <td>{{user.ชื่อ}}</td>
          <td>{{user.สกุล}}</td>
          <td>{{user.อายุ}}</td>
          <td>
            <a
              href="javascript:;"
              class="btn btn-warning"
              v-on:click="deleteUser(user.id,index)"
            >Delete</a>
          </td>
        </tr>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  mounted() {
    this.getUserData();
  },
  methods: {
    getUserData() {
      axios.get("/api/users").then(response => {
        this.users = response.data;
      });
    },
    deleteUser(id,index) {
      axios.delete('/api/users/'+id).then(response => {
        console.log(id);
        this.users.splice(index,1);
      });
    }
    // deleteUser(id) {
    //  console.log(id);
    // }
  },

  data() {
    return {
      users: [],
      user: {
        id: 0,
        ชื่อ: "",
        สกุล: "",
        อายุ: ""
      }
    };
  }
};
</script>

<style>
</style>
