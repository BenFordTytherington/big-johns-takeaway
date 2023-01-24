<template>
  <div class="container">
    <h1>大约翰的大外卖 Big Johns Big Takeaway 大约翰的大外卖</h1>
    <div class="three">
      <Renderer ref="renderer" class="john" resize="true" :orbitCtrl="true">
        <Camera :position="{y: 4, z: 12}" ref="camera"/>
        <Scene background="#A60A27">
          <GltfModel ref="head" :position="{y: -2}"
      src="free_basemesh_head_fat_man.glb"
      @load="onReady"
      @progress="onProgress"
      @error="onError"
          />
          <AmbientLight intensity="0.5"/>
          <PointLight :intensity="(Math.random() / 2) + 0.5" :position="{x: 8 * Math.random() - 4, y: 8 * Math.random() - 4, z: 8 * Math.random() - 4}" v-for="_ in 8" />
        </Scene>
      </Renderer>
    </div>
    <div class="products container">
      <div class="item">
        <h2> PICKLED EGGS - £6.75 </h2>
        <img src="https://i5-richmedia.walmartimages.com/asr-rm/97d97c45-8d75-4e54-9d1b-541751aaa57b_360_merchant_manual_2.jpg" alt="">
        <div class="flex-row">
          <input type="number" id="eggs" value="1">
          <button @click="this.addProduct('Pickled Eggs', 6.75, 'eggs')">ADD TO ORDER</button>
        </div>
      </div>

      <div class="item">
        <h2> KUNG PO SEAL - £8.25 </h2>
        <img src="https://d.newsweek.com/en/full/1553863/seal-pup-norfolk-england.jpg?w=600&q=75&f=920bf526fe05f3ddedd2404280c8cfb2" alt="">
        <div class="flex-row">
          <input type="number" id="seal" value="1">
          <button @click="this.addProduct('Kung Po Seal', 8.25, 'seal')">ADD TO ORDER</button>
        </div>
      </div>

      <div class="item">
        <h2> FOD SWEAT SALSA - £2.50 </h2>
        <img src="https://www.simplyrecipes.com/thmb/ylokGuLiW69OUFyeYl410An882g=/1500x0/filters:no_upscale():max_bytes(150000):strip_icc()/__opt__aboutcom__coeus__resources__content_migration__simply_recipes__uploads__2019__07__Fresh-Tomato-Salsa-LEAD-2-2699ad8059ba4067b222c742bcf318da.jpg" alt="">
        <div class="flex-row">
          <input type="number" id="salsa" value="1">
          <button @click="this.addProduct('Fod Sweat Salsa', 2.99, 'salsa')">ADD TO ORDER</button>
        </div>
      </div>

      <div class="item">
        <h2> PIGS LIP CHOW MEIN - £5.50 </h2>
        <img src="https://dehayf5mhw1h7.cloudfront.net/wp-content/uploads/sites/1188/2019/12/02131458/PigLips.png" alt="">
        <div class="flex-row">
          <input type="number" id="lips" value="1">
          <button @click="this.addProduct('Pigs Lips Chow Mein', 5.59, 'lips')">ADD TO ORDER</button>
        </div>
      </div>
      
      <div class="item">
        <h2> HOISIN CRISPY OWL - £10.75 </h2>
        <img src="data:image/jpeg;base64,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" alt="">
        <div class="flex-row">
          <input type="number" id="owl" value="1">
          <button @click="this.addProduct('Hoisin Crispy Owl', 10.75, 'owl')">ADD TO ORDER</button>
        </div>
      </div>

      <button @click="placeOrder()">
        SUBMIT ORDER
      </button>

    </div>
    <div class="summary">
      <p id="orderText">
        NO ITEMS IN ORDER
      </p>
    </div>

  </div>
  
</template>

<script>

import {
  Renderer,
  Scene,
  Camera,
  GltfModel,
  AmbientLight,
  PointLight
} from '/troisjs'

export default {
  mounted() {
    const renderer = this.$refs.renderer;
    const orbitC = renderer.three.cameraCtrl;
    orbitC.autoRotate = true;
    orbitC.autoRotateSpeed = 10;
    orbitC.enabled = false;

  },

  data() {
    return {
      order: []
    }
  },

  components: {
    Renderer,
    Camera,
    Scene,
    GltfModel,
    AmbientLight,
    PointLight
  },
  methods: {
    addProduct(name, price, ID) {
      let quantity = document.getElementById(ID).value;
      this.order.push(
        {
          name: name,
          price: price,
          quantity: quantity
        }
      )
    },

    placeOrder() {
      let text = document.getElementById("orderText");
      text.textContent = '';
      for (let i = 0; i < this.order.length; i++) {

        let quantity = this.order[i].quantity;
        let name = this.order[i].name;
        let price = this.order[i].price;

        text.textContent += `${quantity} X ${name} - £${price * quantity} \r\n \r\n`
      }
      text.textContent += `Total: £${this.calculatePrice()}`

    },

    calculatePrice() {
      let sum = 0;

      for (let i = 0; i < this.order.length; i++) {
        sum += this.order[i].price * this.order[i].quantity;
      }

      return sum;
    }
  }
};

</script>