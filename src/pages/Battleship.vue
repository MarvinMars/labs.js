<template>
    <q-page class="flex flex-center column items-center" :style="returnBG('bg')">
        <div class="row items-center justify-center q-gutter-sm">
            <div class="col-md-3" v-for="( item , index ) in map" :key="index">
                <q-img class="tile" @click="fire( item, index )" :src="getImage(item)"></q-img>
            </div>
        </div>
        <div class="row items-center justify-center">
            <div class="col-12">
                <h3 class="text-center" style="color: #52352a">Available Hits</h3>
            </div>
            <div class="col-1" v-for="(hit, index) in availableHits" :key="index">
                <q-img class="tile" :src="returnUrl('bomb.svg')" contain></q-img>
            </div>
        </div>
    </q-page>
</template>

<script>
export default {

  name: 'Battleship',

  data(){
    return {
        map: [ 0, 0, 0, 0, 0, 0, 0, 0, 0 ],                       /* 3x3 map; 0 - empty; 1 - ship; 2 - hit */
        hits: 0,                                                  /* hits on the map */
        max_hits: 8,                                              /* hits on the map */
        location: 0,                                              /* ship location on the map */
        status_array: [ 'success', 'error', 'warning', 'info' ],  /* labels for status */
        status_num: 3,                                            /* status of game */
        title: '',                                                /* title for alert */
        msg: '',                                                  /* message for alert */
        gameStatus: true,                                          /* added class when game is end for showing ship */
        /* markers */
        empty: 0,
        ship: 1,
        hit: 2,
        ship_crashed: 3
    }
 },

  watch:{
    hits(){
        if( this.hits >= this.max_hits ){
            this.lose()
        }
    }
  },

  mounted(){
    this.start();
  },

  computed:{
    status(){
      return this.status_array[ this.status_num ];
    },
      availableHits(){
          return this.max_hits - this.hits;
      }
  },

  methods:{
    start(){
      this.location = this.getPosition(9);
      this.$set(this.map, this.location, this.ship);
      this.status_num = 3;
      this.title = 'Игра началась!';
      this.msg = '';

      this.showAlert();
    },

    end(){
        this.gameStatus = false;
    },

    win(){
        this.title = 'В яблочко!';
        this.msg = 'Ты победитель';
        this.status_num = 0;
        this.showAlert();
        this.end();
    },

    lose(){
        this.title = 'Проиграл';
        this.msg = 'Игра закончена';
        this.status_num = 1;
        this.changeMap(this.location, this.ship);
        this.showAlert();
        this.end();
    },

    reset(){
        let _this = this;
        this.$swal('Еще поиграем?','','question')
        .then((result) => {
            if (result.value) {
                _this.location = 0;
                _this.hits = 0;
                _this.gameStatus = true;
                _this.map = [ 0, 0, 0, 0, 0, 0, 0, 0, 0 ];
                _this.start();
            }
        });
    },

    changeMap(index, value){
        this.$set(this.map, index, value);
    },

    tick(item){
        this.changeMap(item,this.hit);
        this.hits++;
    },

    checkMap(){
        let _this = this;

        let result = this.map.some(function(element) {
          /* if u dont have empty cards for shots, game is over */
          if ( element === _this.empty ) {
              return true;
          }

          return false;
        });

        /**
        *   Or we can add something like this shots === 8
        *   Im added it in watch method
        * */

        if( !result ){
            this.lose();
        }

    },

    fire( item, hit ){

      if( !this.gameStatus ){
          this.reset();
          return false;
      }

      switch (item) {
        case this.empty :

          this.title = 'Мимо';
          this.msg = 'Играем дальше';
          this.status_num = 3;

          this.tick(hit);
          break;
        case this.ship :
            this.changeMap(hit, this.ship_crashed);
            this.win();
            break;
        case this.hit :

          this.title = 'Забыл?';
          this.msg = 'Ты уже стрелял сюда!';
          this.status_num = 2;

          this.tick(hit);
          break;
      }

      this.checkMap();
      this.showAlert();
    },

      getImage(item){
          let image = '';

          switch (item) {
              case this.empty:
                  image = 'waves' ;
                  break;
              case this.ship:
                  image = 'galleon' ;
                  if( this.gameStatus ) image = 'waves';
                  break;
              case this.ship_crashed:
                  image = 'ship-wreck' ;
                  break;
              case this.hit:
                  image = 'cross-mark' ;
                  break;
          }

          return this.returnUrl(image + '.svg');
      },

    returnBG(imageName){
        return {
            backgroundImage: 'url(\''+ this.returnUrl( imageName+'.jpg' ) +'\') !important',
            backgroundRepeat: 'no-repeat',
            backgroundPosition: 'center center',
            backgroundSize: 'cover',
        };
    },
      returnUrl(imageName){
          return  require('../statics/'+imageName);
      },

    showAlert(){
      this.$swal( this.title, this.msg, this.status );
    },

    getPosition(max) {
      return Math.floor(Math.random() * Math.floor(max));
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .tile {
      min-width: 50px ;
      min-height: 50px;
      cursor: pointer;
  }

</style>
