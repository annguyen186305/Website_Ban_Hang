<template>
  <div>
    <div class="cart">Giỏ hàng ({{ cart.length }})</div>
    <div v-if="cart.length > 0" class="cart-details">
      <h3>Chi tiết giỏ hàng</h3>
      <table>
        <thead>
        <tr>
          <th>Hình ảnh</th>
          <th>Tên sản phẩm</th>
          <th>Màu sắc</th>
          <th>Kích thước</th>
          <th>Giá</th>
          <th>Thao tác</th>
        </tr>
        </thead>
        <tbody>
        <tr v-for="(item, index) in cart" :key="index">
          <td><img :src="item.image" alt="" width="50"></td>
          <td>{{ item.title }}</td>
          <td>{{ item.textColor }}</td>
          <td>{{ item.size }}</td>
          <td>{{ item.price }}</td>
          <td>
            <button @click="handleRemoveItem(index)">Xóa</button>
          </td>
        </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  name: "gioHang",
  props: {
    cart: Array
  },
  methods: {
    handleRemoveItem(index) {
      this.$emit('remove-item', index); // Gửi sự kiện về component cha để xóa sản phẩm khỏi giỏ hàng
    }
  }
};
</script>

<style scoped>
.cart-details {
  margin-top: 20px;
}

.cart-details table {
  width: 100%;
  border-collapse: collapse;
}

.cart-details th,
.cart-details td {
  border: 1px solid #ddd;
  padding: 8px;
  text-align: left;
}

.cart-details th {
  background-color: #f2f2f2;
}
</style>
