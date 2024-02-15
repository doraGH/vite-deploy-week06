<template>
  <h2>後台管理頁面</h2>
  <nav>
    <RouterLink to="/">返回前台</RouterLink> |
    <RouterLink to="/admin/products">後台產品列表</RouterLink> |
    <RouterLink to="/admin/order">後台訂單列表</RouterLink>
  </nav>
  <hr>
  <RouterView></RouterView>
</template>

<script>
import axios from 'axios';
import Swal from 'sweetalert2';

const { VITE_URL } = import.meta.env;

export default {
  methods: {
    mounted() {
    // 取得暫存在cookie的 Token
      const token = document.cookie.replace(/(?:(?:^|.*;\s*)hexToken\s*=\s*([^;]*).*$)|^.*$/, '$1');
      axios.defaults.headers.common.Authorization = token;

      // 確認是否登入狀態
      this.checkLogin();
    },
    // 確認是否登入
    checkLogin() {
      const url = `${VITE_URL}/api/user/check`;
      axios.post(url)
        .then((response) => {
          Swal.fire(response.data.success);
        })
        .catch((error) => {
          Swal.fire(error.response.data.message);
          this.$router.push('/login');
        });
    },
  },

};
</script>
