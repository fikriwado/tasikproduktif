<template>
   <div class="container">
      <div class="row justify-content-center">
         <div class="col-12 col-sm-12 col-md-10 col-lg-10 col-xl-10 text-center">
            <h1 class="title-web">Tasik Produktif</h1>
            <p class="tagline-web">Banyak orang hebat tersembunyi di Tasik, ayo kita merge</p>
            <div class="devider"></div>
            <div class="tag-list">
               <a v-for="(link,index) in linkReal" :key="index" :href="link.url" class="btn-tag" :class="[link.teks, {active: link.active == true}]" @click="ubahKategori(link.teks)">{{link.show}}</a>
            </div>
         </div>
      </div>

      <div class="row justify-content-center">
         <div class="col-12 col-sm-12 col-md-10 col-lg-10 col-xl-10" v-if="filterPostsList.length>0">
            <div class="list-produktif" v-for="(post, index) in filterPostsList.slice(0,this.limit)" :key="index">
               <div class="clearfix">
                  <div class="thumbnail-produktif float-left">
                     <img :src="post.images" class="d-block w-100 img-fluid">
                  </div>
                  <div class="wrap-text-produktif float-left">
                     <h3 class="title-produktif text-capitalize">{{post.judul}}</h3>
                     <p class="desc-produktif">{{post.deskripsi}}</p>
                     <a :href="post.instagram" class="btn-tag text-uppercase" target="_blank" v-if="post.instagram!=''">instagram <i class="fab fa-instagram"></i></a>
                     <a :href="post.website" class="btn-tag text-uppercase" target="_blank" v-if="post.website!=''">website <i class="fas fa-globe"></i></a>
                  </div>
               </div>
            </div>
            <div class="btn-load-more text-center" @click="addlimit()">Lihat Lainnya</div>
         </div>
         <div class="col-12 col-sm-12 col-md-10 col-lg-10 col-xl-10" v-else>
            <h3 class="title-produktif text-capitalize text-center text-danger">Yah, datanya tidak ada nih. maaf ya,,,</h3>
         </div>
      </div>

      <div class="row justify-content-center">
         <div class="col-12 col-sm-12 col-md-10 col-lg-10 col-xl-10">
            <h4 class="title-about mb-3">Tentang</h4>
               <p class="desc-about">
                  <span class="d-inline-block mb-2">Tasik Produktif adalah sebuah website tempat mengumpulkan data komunitas, cafe, working space dan lainnya yang ada di Kota Tasikmalaya, dengan tujuan menjadikan Kota Tasikmalaya sebagai Kota Produktif dimulai dari hal Terkecil.</span><br/>
                  <span class="d-inline-block mb-2">Kamu bias mendaftarkan komunitas positif kamu di Tasik Produktif <a href="https://forms.gle/LzBGDawZvYD9VzjLA" target="_blank">lewat sini</a> agar banyak orang yang bergabung dan melakukan hal baik di komunitas kamu.</span><br/>
                  <span class="d-inline-block mb-2">Tasik Produktif dibuat oleh <a href="https://www.instagram.com/fikriwado_" target="_blank">Moch Fikri Khoirurrizal</a> dengan ide mengikuti ide dari Kota Makasar yaitu <a href="https://littlemakassar.com/" target="_blank">Little Makassar</a> yang dibuat oleh <a href="https://hilman.space/" target="_blank">Hilman Ramadhan</a>.</span><br>
                  <span>Jika kamu suka dengan website informasi ini, silahkan share kepada yang lain. <a href="http://bit.ly/tasikproduktif" target="_blank">bit.ly/tasikproduktif</a></span>
               </p>
         </div>
      </div>
   </div>
</template>

<script>
import dataPostList from '../postlist.js'

export default {
   name: 'Home',
   data() {
      return {
         posts: dataPostList,
         links: [],
         kategori: '',
         limit: 5
      }
   },
   methods: {
      ubahKategori(kategori) {
         let semuaMenu = document.getElementsByClassName('btn-tag')
         let menuAktif = document.getElementsByClassName(kategori)
         semuaMenu.forEach((item) => {
            item.classList.remove('active')
         });
         menuAktif[0].classList.add('active')
         this.limit = 5
         return this.kategori = kategori
      },
      addlimit() {
         return this.limit += 5
      }
   },
   computed: {
      filterPostsList() {
         if ( this.kategori == 'semua' ) {
            return this.posts
         }else {
            return this.posts.filter(post => post.kategori === this.kategori)
         }
      },
      filterKategori() {
         return this.kategori
      },
      activeKategori(teks) {
         if (this.kategori == teks) {
            return true
         }else {
            return false
         }
      },
      linkReal() {
         return this.links
      }
   },
   mounted() {
      if ( window.location.hash == '' ){
         this.kategori = 'semua'
      }else{
         this.kategori = window.location.hash.substr(1)
      }

      this.links = [
         {url: '#semua', teks: 'semua', show: 'Semua', active: this.kategori == 'semua' ? true : false },
         {url: '#komunitas', teks: 'komunitas', show: 'Komunitas', active: this.kategori == 'komunitas' ? true : false},
         {url: '#cafe', teks: 'cafe', show: 'Cafe', active: this.kategori == 'cafe' ? true : false},
         {url: '#workingspace', teks: 'workingspace', show: 'Working Space', active: this.kategori == 'workingspace' ? true : false},
         {url: '#startup', teks: 'startup', show: 'Startup', active: this.kategori == 'startup' ? true : false},
         {url: '#bisnis', teks: 'bisnis', show: 'Bisnis', active: this.kategori == 'bisnis' ? true : false},
         {url: '#media', teks: 'media', show: 'Media', active: this.kategori == 'media' ? true : false},
         {url: '#kesehatan', teks: 'kesehatan', show: 'Kesehatan', active: this.kategori == 'kesehatan' ? true : false},
         {url: '#lainnya', teks: 'lainnya', show: 'Lainnya', active: this.kategori == 'lainnya' ? true : false}
      ]
   }
}
</script>
