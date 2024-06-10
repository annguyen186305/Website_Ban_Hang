<template>
  <div>
    <header>
      <h1>Dép quai ngang MOOVER AUTHENTIC</h1>
    </header>
    <div class="container">
      <gio-hang :cart="cart" @remove-item="handleRemoveItem" />
    <div class="product">
      <div class="product-image">
        <div class="image">
          <img :src="getProduct.image" alt="">
        </div>
      </div>
      <div class="product-content">
        <h3 class="title">
          <a :href="url" :target="target">{{ title }}</a>
        </h3>
        <p class="brand">Thương hiệu: No brand</p>
        <p class="quantity" v-if="getProduct.quantity > 0">Còn lại: {{ getProduct.quantity }} Sản phẩm</p>
        <p class="quantity" v-if="getProduct.quantity <= 0">Sản phẩm đã hết hàng</p>
        <div class="wrapper-price">
          <div class="final-price">{{ formatFinalPrice }}</div>
          <div class="origin-price">{{ formatOriginalPrice }}</div>
          <div class="sale-price">-{{ sale * 100 }}%</div>
        </div>
        <div class="wrapper-color">
          <div class="text">Màu sắc</div>
          <div class="list-color">
            <p class="color-text">{{ getProduct.textColor }}</p>
            <ul>
              <li
                  v-for="(item, index) in listProductDetail"
                  :class="classActive(index)"
                  :key="index"
                  @click="handleClickColor($event, index)">
                <img :src="item.image" :alt="item.textColor">
              </li>
            </ul>
          </div>
        </div>
        <div class="wrapper-size">
          <div class="text">Kích thước</div>
          <div class="list-size">
            <ul>
              <li
                  v-for="(size, index) in listSize"
                  :class="{ active: selectedSize === size }"
                  :key="index"
                  @click="handleClickSize(size)">
                {{ size }}
              </li>
            </ul>
          </div>
        </div>
        <button
            @click="handleAddToCart" class="add-to-cart">Thêm vào giỏ</button>
        <button @click="handlePurchase" class="purchase-button">Mua hàng</button>
      </div>
    </div>
    <div class="description">
      <ul class="extra-info">
        <li v-for="(item, index) in listDesc" :key="index">{{ item }}</li>
      </ul>
    </div>
    <footer>

        <p> Địa chỉ:ÔNG ÍCH KHIÊM HCM - TP. Hồ Chí Minh </p>
        <p> Nhà sản xuất : BGHOUSE </p>
        <p> Xuất xứ: Việt Nam</p>
    </footer>
  </div>
  </div>
</template>

<script>
import gioHang from "@/components/gioHang.vue";

export default {
  name: "giaoDienChinh",
  components:{
    gioHang
  },
  data() {
    return {
      title: 'Dép quai ngang MOOVER AUTHENTIC, unisex, dễ phối đồ, mang êm chân, đế mang chống trơn trượt',
      url: 'https://shopee.vn/D%C3%A9p-quai-ngang-MOOVER-AUTHENTIC-unisex-d%E1%BB%85-ph%E1%BB%91i-%C4%91%E1%BB%93-mang-%C3%AAm-ch%C3%A2n-%C4%91%E1%BA%BF-mang-ch%E1%BB%91ng-tr%C6%A1n-tr%C6%B0%E1%BB%A3t-i.199558847.16191787061?sp_atk=f1ce3fa4-dd00-4e8d-8e8b-cf122085e901&xptdk=f1ce3fa4-dd00-4e8d-8e8b-cf122085e901',
      target: '_blank',
      price: 280000,
      sale: 0.2,
      selectedProduct: 2,
      selectedSize: '',
      cart: [],
      cardNumber: 1,
      listProductDetail: [
        {
          image: require('@/assets/depTrangChuDen.jpg'),
          quantity: 5,
          textColor: 'Đế Trắng Chữ Đen'
        },
        {
          image: require('@/assets/depDenchuTrang.jpg'),
          quantity: 8,
          textColor: 'Đế Đen Chữ Trắng'
        },
        {
          image: require('@/assets/fullDen.jpg'),
          quantity: 10,
          textColor: 'Màu Đen'
        },
      ],
      listSize:['36','37','38','39','40','41','42','43'],
      listDesc: [
        'Đế: EVA cao cấp, bảo vệ môi trường, êm ái và đàn hồi tốt.',
        'Không biến dạng: Độ bền cao, chống nắng và nước, sử dụng suốt năm.',
        'Quai: Simili bền, Chống nước, chịu thời tiết tốt, lót mút êm ái.',
        'Keo: Keo dán chắc chắn, kết dính tốt.',
        'Cảm giác mang: Dép nhẹ, ôm chân, đế mềm mại và chống trượt.'
      ],
    };
  },
  methods: {
    handleClickColor(e, index) {
      this.selectedProduct = index;
    },
    classActive(index) {
      return {
        active: this.selectedProduct === index
      };
    },
    handleClickSize(size) {
      this.selectedSize = size;
    },
    handleAddToCart(e) {
      if (!this.selectedSize) {
        alert('Vui lòng chọn kích thước');
        return;
      }
      if (this.cart.length + 1 > this.getProduct.quantity) {
        alert('Số lượng không đủ');
      } else {
        this.cart.push({
          title: this.title,
          price: this.formatFinalPrice,
          image: this.getProduct.image,
          textColor: this.getProduct.textColor,
          size: this.selectedSize
        });
        this.cardNumber = this.cart.length;  // Cập nhật số lượng trong giỏ hàng
      }
      console.log(e.target);
    },
    handlePurchase() {
      // Xử lý sự kiện mua hàng ở đây
      alert('Chức năng "Mua hàng" chưa được triển khai');
    },
    handleRemoveItem(index) {
      // Xóa sản phẩm khỏi giỏ hàng dựa trên chỉ số được truyền từ component gioHang
      this.cart.splice(index, 1);
    }
  },
  computed: {
    formatOriginalPrice() {
      var number = this.price;
      return new Intl.NumberFormat('de-DE', { style: 'currency', currency: 'VND' }).format(number);
    },
    formatFinalPrice() {
      var number = this.price - this.sale * this.price;
      return new Intl.NumberFormat('de-DE', { style: 'currency', currency: 'VND' }).format(number);
    },
    getProduct() {
      let index = this.selectedProduct;
      return this.listProductDetail[index];
    }
  }
};
</script>

<style scoped>
body {
  margin: 0;
  font-family: Arial, Helvetica, sans-serif;
}
.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 30px;
}
img {
  max-width: 100%;
}
.product {
  max-width: 700px;
  display: flex;
  margin-top: 20px;
  position: relative;
}
.product .product-image {
  flex-basis: 40%;
  max-width: 40%;
  padding-right: 30px;
}
.product .product-content {
  flex-basis: 60%;
}
.product-image .image {
  width: 100%;
  border: 1px solid #ccc;
}
.product-image .image img {
  display: block;
}
.title {
  margin-top: 0;
}
.title a {
  color: #333;
  text-decoration: none;
}
.cart {
  display: inline-block;
  padding: 15px 10px;
  border: 1px solid #ccc;
}
.wrapper-price .final-price {
  color: #f57224;
  font-weight: 700;
  font-size: 22px;
  margin-bottom: 5px;
}
.wrapper-price .origin-price,
.wrapper-price .sale-price {
  display: inline-block;
  font-size: 14px;
  color: #ccc;
  vertical-align: middle;
}
.wrapper-price .sale-price {
  color: #333;
  margin-left: 5px;
  padding: 3px;
  font-size: 10px;
  border-radius: 5px;
  border: 1px solid #f57224;
}
.wrapper-color {
  display: flex;
  margin-top: 15px;
  padding-top: 15px;
  border-top: 1px solid #eee;
}
.wrapper-color .text {
  width: 100px;
  min-width: 100px;
}
.wrapper-color p {
  margin-top: 0;
  margin-bottom: 10px;
}
.list-color ul {
  list-style-type: none;
  display: flex;
  margin: 0;
  padding: 0;
}
.list-color ul li {
  width: 40px;
  height: 40px;
  border: 1px solid #ccc;
  margin-right: 20px;
}
.list-color ul li:hover,
.list-color ul li:active {
  border-color: #f57224;
}
.description {
  max-width: 700px;
}
.description .extra-info {
  padding-left: 0;
  list-style-position: inside;
}
.add-to-cart {
  border: 1px solid #ffb916;
  background: #ffb916;
  color: #fff;
  display: block;
  padding: 12px 30px;
  margin-top: 30px;
  text-transform: uppercase;
  font-size: 16px;
  cursor: pointer;
}
.purchase-button{
  border: 1px solid #ffb916;
  background: #ffb916;
  color: #fff;
  display: block;
  padding: 12px 30px;
  margin-top: 30px;
  text-transform: uppercase;
  font-size: 16px;
  cursor: pointer;
}
header {
  color: #fff;
  padding: 15px 30px;
  background-color: #3498db;
}
footer {
  color: #fff;
  padding: 15px 30px;
  background-color: #34495e;
}
header h1, footer h1 {
  margin: 0;
}
.wrapper-size {
  display: flex;
  margin-top: 15px;
  padding-top: 15px;
  border-top: 1px solid #eee;
}
.wrapper-size .text {
  width: 100px;
  min-width: 100px;
}
.wrapper-size p {
  margin-top: 0;
  margin-bottom: 10px;
}
.list-size ul {
  list-style-type: none;
  display: flex;
  margin: 0;
  padding: 0;
}
.list-size ul li {
  padding: 5px 10px;
  border: 1px solid #ccc;
  margin-right: 10px;
  cursor: pointer;
}
.list-size ul li:hover,
.list-size ul li.active {
  border-color: #f57224;
}
</style>
