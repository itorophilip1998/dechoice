<template>
  <div>
    <img src="~assets/image/bg.jpg" class="hero">
    <div class="overlay"></div>
    <div class="my-container bg-transparent text-white pt-5 p-2 mt-5">
        <h1 >
            De `Choice Simply Tasty!
        </h1>

        <p class="my-4 text-light">
    WELCOME TO DECHOICE MALL. Dechoice Mall. All Categories, Uncategorized, All Products, Fast Food, Africana, Bakery, Cakes, Chicken & Fish, Continental.
        </p>
        <nuxt-link to="/login" class="btn btn-success rounded-pill w-50 mt-3 shadow  text-white"> Order Now <i class="fa fa-long-arrow-right ml-2" aria-hidden="true"></i></nuxt-link>
      
    </div>
  </div>
</template>


<script>
localStorage.setItem('wallet',0)

export default {
}
</script>

<style >
    .hero{
      /* background-image:url("~assets/images/hero.jpg"); */
      height:100vh;
      position: fixed;
      background-size: cover;
    }
    .my-container{
      z-index: 4 !important;
      position: absolute;
      top:0;  left:0;  bottom:0;
      padding-top:32% !important;

    }
    .contact>.fa{
      margin-left: 4px;
      background:var(--success) !important;
      border-radius: 50%;
      width: 27px;
      height: 27px;
      line-height: 1.7;
    }
    .contact{
      bottom:0;
      position:absolute;
      width: 100%;
    }
</style>


