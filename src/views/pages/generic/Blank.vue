<template>
  <div class="content">
     <b-pagination
          @change="onPageChanged"
          :total-rows="totalRows"
          :per-page="perPage"
          v-model="currentPage"
          class="my-0"
        />
    <gallery
      :images="paginatedItems"
      :index="index"
      :options="{ indicatorOptions: { thumbnailIndicators: true } }"
      @close="index = null"
    ></gallery>
     <b-row>
        <b-col sm="9">
    <b-row class="items-push">
      <b-col
        md="6"
        lg="4"
        xl="3"
        class="animated fadeIn"
        v-for="(item, itemIndex) in paginatedItems"
        :key="itemIndex"
      >
        <b-form-checkbox size="lg" v-model="imagesSelected[item]" @click="imagesSelected[item]=true"></b-form-checkbox>
        <!-- <input class="checkbox" type="checkbox" @click.self="imagesSelected[photoIndex] = !imagesSelected[photoIndex]" id="vehicle1" name="vehicle1" :value="imagesSelected[photoIndex]" > -->
        <a
          class="img-link img-link-zoom-in img-thumb"
          href="javascript:void(0)"
          @click="index = itemIndex"
        >
          <img
            class="img-fluid"
            :src="item"
            alt="Photo"
            style="position: relative; z-index: 2"
          />
        </a>
      </b-col>
        </b-row>
        </b-col>
        <b-col sm="3">
         <b-card         
         
          text-variant="black"
          
          class="text-center"
          >
          <p class="card-text">
            {{imagesToDo}}
          </p>
        </b-card>  
        </b-col>
      
      <!-- <b-col
        cols="12"
        sm="4"
        class="my-1"
        :key="index"
        v-for="(item, index) in paginatedItems"
      >
        <b-card
         
          :header="item"
          class="text-center"
        >
          <p class="card-text">
            {{ item.body }}
          </p>
        </b-card>
      </b-col> -->
    </b-row>

    
  </div>
</template>

<script>
import VueGallery from "vue-gallery";
import {chunk,forIn} from 'lodash';
const items = [
  "img/laptop/laptop1.jpg",
  "img/laptop/laptop2.jpg",
  "img/laptop/laptop3.jpg",
  "img/laptop/laptop4.jpg",
  "img/laptop/laptop5.jpg",
  "img/laptop/laptop6.jpg",
  "img/laptop/laptop7.jpg",
  "img/laptop/laptop8.jpg",
  "img/laptop/laptop9.jpg",
  "img/laptop/laptop10.jpg",
  "img/laptop/laptop11.jpg",
  "img/laptop/laptop12.jpg",
  "img/laptop/laptop13.jpg",
  "img/laptop/laptop14.jpg",
  "img/laptop/laptop15.jpg",
  "img/laptop/laptop16.jpg",
];

export default {
  components: {
    gallery: VueGallery,
  },
  name: "MyBootstrapGrid",
  data() {
    return {
      imagesSelected: {},
      index:null,
      items: items,
      paginatedItems: items,
      perPage: 8,
      totalRows: items.length,
      currentPage: 1,
    };
  },
  computed: {
    pageCount() {
      let l = this.totalRows,
        s = this.perPage;
      return Math.floor(l / s);
    },
    chunkedPhotos(){
      return chunk(items,this.perPage);
    },
    imagesToDo(){
      let im = [];
      forIn(this.imagesSelected,(value,key)=>{
        if(value===true){
          im.push(key);
        }
      });
      return im;
    }
   
  },
  mounted() {
   this.paginatedItems=this.chunkedPhotos[0];
  },
  methods: {
    
    onPageChanged(page) {
      // this.paginate(this.perPage, page - 1);
      this.paginatedItems=this.chunkedPhotos[page-1];
    },
    test(){
      console.log("check");
    }
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>