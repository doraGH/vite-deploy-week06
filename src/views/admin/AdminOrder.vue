<template>
  <VueLoading :active="isLoading" />
  <h2>訂單列表</h2>
  <div class="container">
    <div class="mt-4">
      <div class="text-end">
      <button class="btn btn-outline-danger" type="button">清空訂單</button>
      </div>
    </div>
    <div class="bg-light my-4 p-4">
      <table class="table align-middle">
        <thead>
          <tr>
            <th>訂單編號</th>
            <th>訂單日期</th>
            <th>訂單總金額</th>
            <th>是否付款</th>
            <th>查看訂單</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="item in orders" :key="item.id">
            <td>{{ item.id }}</td>
            <td>{{ item.create_at }}</td>
            <td>
              <span :class="{'text-success': item.is_paid}">
              {{ item.is_paid ? '已付款' : '未付款' }}</span>
            </td>
            <td>{{ item.total }}</td>
            <td>
              <div class="btn-group">
                <button type="button" class="btn btn-outline-primary btn-sm"
                @click.prevent="openProductModal('edit', item)">
                <font-awesome-icon :icon="['fas', 'eye']" /> 編輯
                </button>
                <button type="button" class="btn btn-outline-danger btn-sm"
                @click.prevent="openProductModal('delete', item)">
                  刪除
                </button>
              </div>
            </td>
          </tr>
        </tbody>
      </table>
      <!-- pagination 分頁 -->
      <PaginationComponent :pages="pagination" @change-page="getOrders"></PaginationComponent>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import Swal from 'sweetalert2';

import PaginationComponent from '@/components/PaginationComponent.vue';

const { VITE_URL, VITE_PATH } = import.meta.env;

export default {
  data() {
    return {
      orders: [],
      pagination: {},
      isLoading: false,
    };
  },
  components: {
    PaginationComponent,
  },
  methods: {
    // 取得訂單
    getOrders(page = 1) {
      const url = `${VITE_URL}/api/${VITE_PATH}/admin/orders?page=${page}`;
      this.isLoading = true;
      axios
        .get(url)
        .then((response) => {
          const { orders, pagination } = response.data;
          this.isLoading = false;
          this.orders = orders;
          this.pagination = pagination;
        })
        .catch((error) => {
          Swal.fire(error.response.data.message);
          this.$router.push('/login');
        });
    },
  },
  mounted() {
    this.getOrders();
  },
};
</script>
