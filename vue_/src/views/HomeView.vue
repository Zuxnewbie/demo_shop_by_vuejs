<template>
  <!-- Featurs Section Start -->
  <div class="container-fluid featurs py-5">
    <div class="container py-5">
      <div class="row g-4">
        <div class="col-md-6 col-lg-3">
          <div class="featurs-item text-center rounded bg-light p-4">
            <div
              class="featurs-icon btn-square rounded-circle bg-secondary mb-5 mx-auto"
            >
              <i class="fas fa-car-side fa-3x text-white"></i>
            </div>
            <div class="featurs-content text-center">
              <h5>Free Shipping</h5>
              <p class="mb-0">Free on order over $300</p>
            </div>
          </div>
        </div>
        <div class="col-md-6 col-lg-3">
          <div class="featurs-item text-center rounded bg-light p-4">
            <div
              class="featurs-icon btn-square rounded-circle bg-secondary mb-5 mx-auto"
            >
              <i class="fas fa-user-shield fa-3x text-white"></i>
            </div>
            <div class="featurs-content text-center">
              <h5>Security Payment</h5>
              <p class="mb-0">100% security payment</p>
            </div>
          </div>
        </div>
        <div class="col-md-6 col-lg-3">
          <div class="featurs-item text-center rounded bg-light p-4">
            <div
              class="featurs-icon btn-square rounded-circle bg-secondary mb-5 mx-auto"
            >
              <i class="fas fa-exchange-alt fa-3x text-white"></i>
            </div>
            <div class="featurs-content text-center">
              <h5>30 Day Return</h5>
              <p class="mb-0">30 day money guarantee</p>
            </div>
          </div>
        </div>
        <div class="col-md-6 col-lg-3">
          <div class="featurs-item text-center rounded bg-light p-4">
            <div
              class="featurs-icon btn-square rounded-circle bg-secondary mb-5 mx-auto"
            >
              <i class="fa fa-phone-alt fa-3x text-white"></i>
            </div>
            <div class="featurs-content text-center">
              <h5>24/7 Support</h5>
              <p class="mb-0">Support every time fast</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
  <!-- Featurs Section End -->

  <!-- Fruits Shop Start-->
  <div class="container-fluid fruite py-5">
    <div class="container py-5">
      <div class="tab-class text-center">
        <div class="row g-4">
          <div class="col-lg-4 text-start">
            <h1>Our Organic Products</h1>
          </div>
          <div class="col-lg-8 text-end">
            <ul class="nav nav-pills d-inline-flex text-center mb-5">
              <li class="nav-item">
                <a
                  class="d-flex m-2 py-2 bg-light rounded-pill active"
                  data-bs-toggle="pill"
                  href="#tab-1"
                >
                  <span class="text-dark" style="width: 130px"
                    >All Products</span
                  >
                </a>
              </li>

              <li class="nav-item">
                <a
                  class="d-flex m-2 py-2 bg-light rounded-pill"
                  data-bs-toggle="pill"
                  href="#tab-2"
                >
                  <span class="text-dark" style="width: 130px"
                    >Best Seller</span
                  >
                </a>
              </li>
            </ul>
          </div>
        </div>
        <div class="tab-content">
          <div id="tab-1" class="tab-pane fade show p-0 active">
            <div class="row g-4">
              <div class="col-lg-12">
                <div class="row g-4">
                  <div
                    class="col-md-6 col-lg-4 col-xl-3"
                    v-for="index in this.productSize"
                    :key="index"
                  >
                    <ProductBox :product="products[index - 1]" />
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div id="tab-2" class="tab-pane fade show p-0">
            <div class="row g-4">
              <div class="col-lg-12">
                <div class="row g-4">
                  <div class="col-md-6 col-lg-4 col-xl-3">
                    <div class="rounded position-relative fruite-item">
                      <div class="fruite-img">
                        <img
                          src="img/fruite-item-5.jpg"
                          class="img-fluid w-100 rounded-top"
                          alt=""
                        />
                      </div>
                      <div
                        class="text-white bg-secondary px-3 py-1 rounded position-absolute"
                        style="top: 10px; left: 10px"
                      >
                        Fruits
                      </div>
                      <div
                        class="p-4 border border-secondary border-top-0 rounded-bottom"
                      >
                        <h4>Grapes</h4>
                        <p>
                          Lorem ipsum dolor sit amet consectetur adipisicing
                          elit sed do eiusmod te incididunt
                        </p>
                        <div
                          class="d-flex justify-content-between flex-lg-wrap"
                        >
                          <p class="text-dark fs-5 fw-bold mb-0"></p>
                          <a
                            href="#"
                            class="btn border border-secondary rounded-pill px-3 text-primary"
                            ><i
                              class="fa fa-shopping-bag me-2 text-primary"
                            ></i>
                            Add to cart</a
                          >
                        </div>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
  <!-- Fruits Shop End-->
</template>

<script>
// import CategoryBox from "../components/Category/CategoryBox.vue";
import ProductBox from "../components/ProductBox.vue";

export default {
  name: "HomeView",
  components: { ProductBox },
  props: ["categories", "products"],
  data() {
    return {
      categorySize: 0,
      productSize: 0,
    };
  },
  mounted() {
    this.categorySize = Math.min(6, this.categories.length);
    this.productSize = Math.min(8, this.products.length);
  },

};
</script>

<style></style>
