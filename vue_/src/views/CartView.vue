<template>
  <!-- Cart Page Start -->
  <div class="container-fluid py-5">
    <div class="container py-5">
      <div class="table-responsive">
        <table class="table">
          <thead>
            <tr>
              <th scope="col">Products</th>
              <th scope="col">Name</th>
              <th scope="col">Price</th>
              <th scope="col">Quantity</th>
              <th scope="col">Total</th>
              <th scope="col">Handle</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="itemCart in cart" :key="itemCart.id">
              <th scope="row">
                <div class="d-flex align-items-center">
                  <img
                    :src="itemCart.imageURL"
                    class="img-fluid me-5 rounded-circle"
                    style="width: 80px; height: 80px"
                    alt=""
                  />
                </div>
              </th>
              <td>
                <p class="mb-0 mt-4">{{ itemCart.productName }}</p>
              </td>
              <td>
                <p class="mb-0 mt-4">
                  {{ formatCurrencyVND(itemCart.price) }}
                </p>
              </td>
              <td class="soluong">
                <div
                  class="input-group quantity mt-4"
                  style="width: 100px; margin: 0 auto"
                >
                  <!-- <div class="input-group-btn">
                    <button
                      class="btn btn-sm btn-minus rounded-circle bg-light border"
                    >
                      <i class="fa fa-minus"></i>
                    </button>
                  </div> -->
                  <input
                    type="text"
                    class="form-control form-control-sm text-center border-0"
                    v-model="itemCart.quantity"
                  />

                  <!-- <span
                    class="form-control form-control-sm text-center border-0"
                  >
                    {{ itemCart.quantity }}
                  </span> -->

                  <!-- <div class="input-group-btn">
                    <button
                      class="btn btn-sm btn-plus rounded-circle bg-light border"
                    >
                      <i class="fa fa-plus"></i>
                    </button>
                  </div> -->
                </div>
              </td>
              <td>
                <p class="mb-0 mt-4">
                  {{ (total = itemCart.quantity * itemCart.price) }}
                </p>
              </td>
              <td>
                <button
                  @click="deleteItem(itemCart.id)"
                  class="btn btn-md rounded-circle bg-light border mt-4"
                >
                  <i class="fa fa-times text-danger"></i>
                </button>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
      <div class="mt-5">
        <input
          type="text"
          class="border-0 border-bottom rounded me-5 py-3 mb-4"
          placeholder="Coupon Code"
          v-model="couponCode"
        />
        <button
          class="btn border-secondary rounded-pill px-4 py-3 text-primary"
          type="button"
          @click="applyCoupon"
        >
          Apply Coupon
        </button>
      </div>
      <div class="row g-4 justify-content-end">
        <div class="col-8"></div>
        <div class="col-sm-8 col-md-7 col-lg-6 col-xl-4">
          <div class="bg-light rounded">
            <div class="p-4">
              <h1 class="display-6 mb-4">
                Cart <span class="fw-normal">Total</span>
              </h1>
              <div class="d-flex justify-content-between mb-4">
                <h5 class="mb-0 me-4">Subtotal:</h5>
                <p class="mb-0">{{ formatCurrencyVND(calculateTotal) }}</p>
              </div>
              <div class="d-flex justify-content-between">
                <h5 class="mb-0 me-4">Coupon</h5>
                <div class="">
                  <p class="mb-0">{{ couponInfo }}</p>
                </div>
              </div>
            </div>
            <div
              class="py-4 mb-4 border-top border-bottom d-flex justify-content-between"
            >
              <h5 class="mb-0 ps-4 me-4">Total</h5>
              <p class="mb-0 pe-4">{{ formatCurrencyVND(adjustedTotal) }}</p>
            </div>

            <router-link
              class="btn border-secondary rounded-pill px-4 py-3 text-primary text-uppercase mb-4 ms-4"
              :to="{ name: 'CheckOut' }"
              type="button"
            >
              Proceed Checkout
            </router-link>
          </div>
        </div>
      </div>
    </div>
  </div>
  <!-- Cart Page End -->
</template>

<script>
import axios from "axios";
// import swal from 'sweetalert';
// import store from "@/store/index.js";


export default {
  name: "CartView",
  props: ["baseURL", "carts"],
  data() {
    return {
      cart: [],
      cartsEmpty: [],
      total: null,
      couponCode: "",
      appliedCoupon: null, // Track the applied coupon
      couponApplied: false,
    };
  },
  created() {
    this.getAll();
  },
  computed: {
    calculateTotal() {
      let total = 0;
      this.cart.forEach((item) => {
        total += item.quantity * item.price;
      });
      return total;
    },
    adjustedTotal() {
      if (this.couponCode.toLowerCase() === "nhan") {
        // Apply 10% discount if the coupon code is "nhan"
        return this.calculateTotal * 0.9; // 10% discount
      } else {
        return this.calculateTotal; // No discount
      }
    },
    couponInfo() {
      if (this.couponCode === "nhan") {
        return "10% discount applied"; // Display coupon information if applied
      } else {
        return "No coupon applied"; // Display if no coupon applied
      }
    },
  },
  methods: {
    clearCart() {
    this.$store.commit('clearCart'); // Call the clearCart mutation
  },
    async getAll() {
      const cartResponse = await axios.get(this.baseURL + "carts");
      this.cart = cartResponse.data;
      console.log(this.cart);
    },

    formatCurrencyVND(amount) {
      return new Intl.NumberFormat("vi-VN", {
        style: "currency",
        currency: "VND",
      }).format(amount);
    },

    applyCoupon() {
      // This method is called when the user clicks on the "Apply Coupon" button
      if (this.couponCode.toLowerCase() === "nhan") {
        this.couponApplied = true; // Set couponApplied to true if the coupon is applied
      } else {
        this.couponApplied = false; // Set couponApplied to false if the coupon is not applied
      }
    },

    deleteItem(id) {
      this.$swal
        .fire({
          title: "Are you sure?",
          text: "You won't be able to revert this!",
          icon: "warning",
          showCancelButton: true,
          confirmButtonColor: "#3085d6",
          cancelButtonColor: "#d33",
          confirmButtonText: "Yes, delete it!",
        })
        .then((result) => {
          if (result.isConfirmed) {
            axios
              .delete(`${this.baseURL}carts/${id}`)
              .then((res) => {
                if (res) {
                  this.$swal.fire({
                    title: "Deleted!",
                    text: "Your dsfdsitem has been deleted.",
                    icon: "success",
                  });
                  this.getAll();
                  // Tải lại dữ liệu hoặc làm bất kỳ thao tác nào cần thiết sau khi xóa
                } else {
                  // Xóa không thành công, xử lý tương ứng
                  this.$swal.fire({
                    title: "Error!",
                    text: "Failed to delete item.",
                    icon: "error",
                  });
                }
              })
              .catch((error) => {
                console.error("Delete error:", error);
                this.$swal.fire({
                  title: "Error!",
                  text: "An error occurred while deleting the item.",
                  icon: "error",
                });
              });
          }
        });
    },
    
  },
};
</script>

<style></style>
