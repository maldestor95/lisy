<template>
    <div >
        <section >
            <img :src="getimgpath('main')" class="main-img" alt=""/>

            <!-- <div v-for="item in days" :key="item.id"
                class="widowframe"
                :style="{ top: item.top ,
                          left:item.left ,
                          width:item.width ,
                          height:item.height
                        }"
                @click="currentimg=item.text;openmodal()"
                >
                <div class="day" :style="{top:item.texttop}">
                        {{item.text}}
                </div>
            </div> -->
            <div class="wrapper">
              <div v-for="item in [1,2,3,4,8,6,6,8,9,10,11,12,13,20,15,16,17,18,19,14,21,22,23,24]"
               :key="item.id"
               @click="currentimg=item;openmodal()"
               >
                {{ item }}
              </div>
            </div>
        </section>

        <div class="modal" :style="{display:displaymodal}">
          <div class="modal-content">
              <img :src="getimgpath(currentimg)" alt="" >
              <v-icon class="white--text topleft " @click="closemodal()">mdi-close</v-icon>
          </div>
        </div>
    </div>
</template>

<script>
export default {
  data() {
    return {
      key: 0,
      imgpath: '2021/fr',
      currentimg: '',
      days: [
        {
          text: 1, top: '10px', left: '10px', width: '100px', height: '150px', texttop: '10px',
        },
        {
          text: 2, top: '150px', left: '150px', width: '150px', height: '150px', texttop: '10px',
        },
      ],
      displaymodal: 'none',

    };
  },
  methods: {
    getimgpath(imgname) {
      const year = this.imgpath.split('/')[0];
      const calendardate = new Date(year, 11, imgname);
      let imgToDisplay = imgname;
      if (imgToDisplay === '') return '';
      if (new Date().getDate() < calendardate.getDate()) imgToDisplay = 'tooearly';

      return `https://maldestor95.github.io/adventpics/${this.imgpath}/${imgToDisplay}.jpg`;
    },
    openmodal() {
      this.displaymodal = 'block';
    },
    closemodal() {
      this.currentimg = '';
      this.displaymodal = 'none';
    },
  },

};
</script>

<style lang="scss" scoped>
$imgradius:8px;
.modal {
  display: none; /* Hidden by default */
  position: fixed; /* Stay in place */
  z-index: 1; /* Sit on top */
  left: 0;
  top: 0;
  width: 100%; /* Full width */
  height: 100%; /* Full height */
  overflow: auto; /* Enable scroll if needed */

  background-color: rgb(0,0,0); /* Fallback color */
  background-color: rgba(0,0,0,0.4); /* Black w/ opacity */
}
.main-img {
    width: 100%;
    object-fit: scale-down;
}
.modal-content {
  background-color: #fefefe;
  position:absolute;
  top:3rem;
  left:10%;
  max-width: 80%;
  padding: 20px;
  border: 0px solid #888;
  border-radius: $imgradius;
}
.topleft {
  position:absolute !important;
    top:0px;
    left: 0px;
    width: 20px;
    background: red !important;
    border-radius: $imgradius 0 $imgradius 0;
}
.modal-content > img {
  max-width: 100%;
  object-fit: scale-down;
  border-radius: $imgradius;
}

.widowframe {
    position: absolute;
    border: 5px dashed white;
    color:white;
    font-size: 5rem;
    margin: auto;
    padding: auto;
    text-align: center;
}
.day{
    position: relative;
}
.wrapper {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-evenly;
  position:absolute;
  top:0px;
}
.wrapper > div {
    border: 5px dashed white;
    color:white;
    font-size: 5rem;
    min-width: 4rem;
    margin: auto;
    padding: 10px;
    text-align: center;
}
.wrapper :nth-child(3n){
  font-size: 6rem;
  border: 1px solid blue;
}
.wrapper :nth-child(2n){
  font-size: 4rem;
  border: 1px solid green;
}
</style>
