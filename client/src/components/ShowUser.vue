<template>
  <div>
    <h1>Show Song</h1>
    <p>id: {{ userId }}</p>
    <p>ชื่อเพลง {{ user.name }} - {{ user.lastname }}</p>
    <p>email: {{ user.email }}</p>
    <p>ชื่อนักร้อง: {{ user.password }}</p>
  </div>
</template>
<script>
import UserService from "@/services/UsersService";
export default {
  data() {
    return {
      user: null,
    };
  },
  async created() {
    try {
      let userId = this.$route.params.userId;
      this.user = (await UserService.show(userId)).data;
    } catch (error) {
      console.log(error);
    }
  },
};
</script>
<style scoped>
</style>