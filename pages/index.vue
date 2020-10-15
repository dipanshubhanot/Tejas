<template>
  <div>
    <div class="section" id="carousel">
      <div class="container">
        <div class="title">
          <h4 align="center">We are MNS, not MSN lol!</h4>
        </div>
        <div class="row">
          <div class="col-12">
            <el-carousel
              height="25rem"
              :interval="2000"
              indicator-position="none"
            >
              <el-carousel-item>
                <img class="d-block" src="img/bg1.jpg" alt="First slide" />
                <div
                  class="carousel-caption d-none d-md-block"
                  style="backgroud: 'rgba(0,0,0,1)'"
                >
                  <h3>Text on a fancy Background</h3>
                </div>
              </el-carousel-item>
              <el-carousel-item>
                <img class="d-block" src="img/bg3.jpg" alt="Second slide" />
                <div class="carousel-caption d-none d-md-block">
                  <h3>Text on a fancy Background</h3>
                </div>
              </el-carousel-item>
              <el-carousel-item>
                <img class="d-block" src="img/bg4.jpg" alt="Third slide" />
                <div class="carousel-caption d-none d-md-block">
                  <h3>Text on a fancy Background</h3>
                </div>
              </el-carousel-item>
            </el-carousel>
          </div>
        </div>
      </div>
    </div> <br>
    <div class="section" >
      <div class="container">
        <div class="title">
          <h4 align="center">Or, you can have these fancy cards for information</h4>
        </div>
        <div class="row">
          <div class="col-12">
            <el-carousel
              height="25rem"
              :interval="2000"
              indicator-position="none"
            >
              <el-carousel-item>
                <card>

                </card>
              </el-carousel-item>
              <el-carousel-item>
                <img class="d-block" src="img/bg3.jpg" alt="Second slide" />
                <div class="carousel-caption d-none d-md-block">
                  <h3>Text on a fancy Background</h3>
                </div>
              </el-carousel-item>
              <el-carousel-item>
                <img class="d-block" src="img/bg4.jpg" alt="Third slide" />
                <div class="carousel-caption d-none d-md-block">
                  <h3>Text on a fancy Background</h3>
                </div>
              </el-carousel-item>
            </el-carousel>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import { Carousel, CarouselItem } from "element-ui";

export default {
  components: {
    [Carousel.name]: Carousel,
    [CarouselItem.name]: CarouselItem,
  },
};
</script>
<style></style>
