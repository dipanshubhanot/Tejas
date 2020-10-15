<template>
  <div class="container-fluid">
    <div class="row">
      <!-- HEADER -->
      <div class="col-lg-12 mx-auto">
        <card type="transparent" class="text-center">
          <template>
            <div class="row">
              <div class="col-sm-6 col-md-6 col-lg-6 d-flex d-sm-block d-lg-block d-md-block">
                <div
                  class="btn-group-toggle w-100"
                  :class="isRTL ? 'float-left' : 'float-right'"
                  data-toggle="buttons"
                >
                  <label
                    v-for="(category, index) in productCategories"
                    :key="category.name"
                    class="btn btn-md btn-default btn-simple btn-round"
                    :class="{ active: currentCategory.activeIndex === index }"
                    :id="index"
                  >
                    <input
                      type="radio"
                      @click="initCategory(index)"
                      :checked="currentCategory.activeIndex === index"
                      autocomplete="off"
                    />
                    <span class="d-none d-sm-block">{{ category.name }}</span>
                    <span class="d-block d-sm-none">{{ category.name }} </span>
                  </label>
                </div>
            </div>
              </div>
          </template>
        </card>
      </div>
      <!-- Products -->

      <div
        v-for="(item, index) in currentItems"
        :key="index"
        class="col-lg-4"
        :class="{ 'text-right': isRTL }"
      >
        <card>
          <img
            slot="image"
            alt="candle"
            height="200rem"
            class="card-img-top"
            :src="item.img"
          />
          <template slot="header">
            <h5 class="card-category">
              Availability : {{ item.quantity }} items
            </h5>
            <h3 class="card-title">
              {{ item.name
              }}<span
              class="btn btn-primary btn-link btn-wd btn-lg"
              style="float:right; font-size:110%">
                <i class="fas fa-rupee-sign"></i> {{ item.price }}</span
              ><br />
            </h3>

            {{ item.desc }} <br /><br /><br />
          </template>
          <template>
            <div class="row">
              <div class="col-sm-5 col-md-5 col-lg-5 text-center">
                <span
                  class="btn btn-icon btn-sm btn-simple col-sm-1 col-md-1 col-lg-1 text-center"
                  @click="decrease_selected_quant(item)"
                >
                  <i class="fas fa-minus"></i
                ></span>
                <span class="btn btn-simple text-center">
                  {{ item.selected_quant }}</span
                >
                <span
                  class="btn btn-icon btn-sm btn-simple col-sm-1 col-md-1 col-lg-1 text-center"
                  @click="increase_selected_quant(item)"
                >
                  <i class="fas fa-plus"></i
                ></span>
              </div>
              <span
                class="btn btn-primary btn-round col-sm-4 col-md-4 col-lg-4"
                @click="
                  addToCart(
                    currentCategory.activeIndex,
                    index,
                    item.selected_quant
                  )
                "
              >
                Add <i class="fas fa-cart-plus"></i
              ></span>
            </div>
            <div class="row">&nbsp;</div>
          </template>
        </card>
      </div>
    </div>
  </div>
</template>
<script>
import config from "@/config";
import { Table, TableColumn } from "element-ui";

export default {
  name: "products",
  components: {
    [Table.name]: Table,
    [TableColumn.name]: TableColumn,
  },
  data() {
    return {
      currentSelection: {
        categoryIndex: -1,
        itemIndex: -1,
        quantity: -1,
      },
      currentCategory: {
        activeIndex: -1,
        items: [],
      },
      user: {
        quantity: 1,
      },
      productCategories: [
        {
          name: "Category1",
          items: [
            {
              name: "Item 1",
              img:
                "https://images.unsplash.com/photo-1537948756265-406a522f1a45?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=633&q=80",
              quantity: 30,
              desc: "Non culpa amet cupidatat est culpa ex adipisicing. Velit non cupidatat nostrud adipisicing ad commodo do sit exercitation ea ad amet. Dolore Lorem aliquip ipsum dolore excepteur dolore laborum sint est non labore. Nulla non irure dolor ipsum eu nulla fugiat. Cillum mollit sunt id minim qui duis minim.",
              price: 150,
              selected_quant: 1
            },
            {
              name: "Item 2",
              img:
                "https://images.unsplash.com/photo-1537948756265-406a522f1a45?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=633&q=80",
              quantity: 30,
              desc: "This is item 2 description",
              price: 150,
              selected_quant: 1
            },
            {
              name: "Item 3",
              img:
                "https://images.unsplash.com/photo-1537948756265-406a522f1a45?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=633&q=80",
              quantity: 30,
              desc: "This is item 3 description",
              price: 150,
              selected_quant: 1
            },
          ],
        },
        {
          name: "Category2",

          items: [
            {
              name: "Item 1",
              img:
                "https://images.unsplash.com/photo-1537948756265-406a522f1a45?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=633&q=80",
              quantity: 30,
              desc: "This is item description",
              price: 150,
              selected_quant: 1
            },
            {
              name: "Item 2",
              img:
                "https://images.unsplash.com/photo-1537948756265-406a522f1a45?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=633&q=80",
              quantity: 30,
              desc: "This is item 2 description",
              price: 150,
              selected_quant: 1
            },
            {
              name: "Item 3",
              img:
                "https://images.unsplash.com/photo-1537948756265-406a522f1a45?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=633&q=80",
              quantity: 30,
              desc: "This is item 3 description",
              price: 150,
              selected_quant: 1
            },
          ],
        },
        {
          name: "Bhintu",

          items: [
            {
              name: "Item 1",
              img:
                "https://images.unsplash.com/photo-1537948756265-406a522f1a45?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=633&q=80",
              quantity: 30,
              desc: "This is item description",
              price: 150,
              selected_quant: 1
            },
            {
              name: "Item 2",
              img:
                "https://images.unsplash.com/photo-1537948756265-406a522f1a45?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=633&q=80",
              quantity: 30,
              desc: "This is item 2 description",
              price: 150,
              selected_quant: 1
            },
            {
              name: "Item 3",
              img:
                "https://images.unsplash.com/photo-1537948756265-406a522f1a45?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=633&q=80",
              quantity: 30,
              desc: "This is item 3 description",
              price: 150,
              selected_quant: 1
            },
          ],
        },
        {
          name: "Bhintu2",
          items: [
            {
              name: "Item 1",
              img:
                "https://images.unsplash.com/photo-1537948756265-406a522f1a45?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=633&q=80",
              quantity: 30,
              desc: "Non culpa amet cupidatat est culpa ex adipisicing. Velit non cupidatat nostrud adipisicing ad commodo do sit exercitation ea ad amet. Dolore Lorem aliquip ipsum dolore excepteur dolore laborum sint est non labore. Nulla non irure dolor ipsum eu nulla fugiat. Cillum mollit sunt id minim qui duis minim.",
              price: 150,
              selected_quant: 1
            },
            {
              name: "Item 2",
              img:
                "https://images.unsplash.com/photo-1537948756265-406a522f1a45?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=633&q=80",
              quantity: 30,
              desc: "This is item 2 description",
              price: 150,
              selected_quant: 1
            },
            {
              name: "Item 3",
              img:
                "https://images.unsplash.com/photo-1537948756265-406a522f1a45?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=633&q=80",
              quantity: 30,
              desc: "This is item 3 description",
              price: 150,
              selected_quant: 1
            },
          ],
        }
      ],
    };
  },
  computed: {
    enableRTL() {
      return this.$route.query.enableRTL;
    },
    isRTL() {
      return this.$rtl.isRTL;
    },
    currentItems() {
      // console.log("Category Changed");
      // return this.currentCategory.activeIndex;
      return this.currentCategory.items;
    },
  },
  watch: {
    currentItems(newValue) {
      console.log("Change watched in currentItems!! -> newIndex:", newValue);
    },
  },
  methods: {
    initCategory(index) {
      this.currentCategory.activeIndex = index;
      this.currentCategory.items = this.productCategories[index].items;
      console.log(this.currentCategory.activeIndex);
    },
    decrease_selected_quant(item){
      if ((item.selected_quant - 1) > 0){
        item.selected_quant--;
      }
      else{
        this.notifyVue('top', 'center', "Order Quantity cannot be 0", 'warning')
      }
    },
    increase_selected_quant(item){
      if((item.selected_quant+1)<= item.quantity){
        item.selected_quant++;
      }
      else{
        this.notifyVue('top', 'center', "Order Quantity cannot exceed Available Quantity", 'warning')
      }
    }
    ,
    addToCart(categoryIndex, itemIndex, quantity) {
      console.log("Category: ", this.productCategories[categoryIndex].name);
      console.log(
        "Item: ",
        this.productCategories[categoryIndex].items[itemIndex].name
      );
      console.log("Order Quantity: ", quantity);
    },
    range(start, end, step = 1) {
      const len = Math.floor((end - start) / step) + 1;
      return Array(len)
        .fill()
        .map((_, idx) => start + idx * step);
    },
    notifyVue(verticalAlign, horizontalAlign, message, color) {
      this.$notify({
        message:
          message,
        timeout: 2000,
        icon: "fas fa-exclamation",
        horizontalAlign: horizontalAlign,
        verticalAlign: verticalAlign,
        type: color
      });
    }
  },
  mounted() {
    this.initCategory(0);
  },
};
</script>
<style></style>
