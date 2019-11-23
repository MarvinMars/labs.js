<template>
    <q-page class="flex flex-center items-center">
        <div class="row items-center justify-center">
            <div class="q-pa-md">
                <div class="q-gutter-md">
                    <q-time v-model="time" format24h/>
                </div>
            </div>
        </div>
        <div class="row items-center justify-center">
            <div class="q-pa-md">
                <q-form @submit="login" class="q-gutter-md">
                    <q-input filled
                            type="string"
                            v-model="inputData.name"
                            label="Name"/>
                    <q-input filled
                            type="password"
                            v-model="inputData.pass"
                            label="Pass"/>
                    <div>
                        <q-btn label="Submit" type="submit" color="primary"/>
                    </div>
                </q-form>

            </div>
        </div>
        <div class="row items-center justify-center" >
            <div class="col-12 text-center row">
                <div class="col-4" v-for="(num, index) in numbers" :key="index">
                    {{ num }}
                </div>
            </div>
            <q-input filled type="number" v-model="num1" label="First"/>
            <q-input filled type="number" v-model="num2" label="Second" />
            <q-input filled type="number" v-model="num3" label="Third" />
        </div>
    </q-page>
</template>

<script>
export default {

  name: 'Battleship',

  data(){
    return {
        time: '',
        num1:0,
        num2:0,
        num3:0,
        inputData:{
            name: '',
            pass: ''
        },
        users: [
            {
                name: 'ivan',
                pass: '333'
            },
            {
                name: 'ssss',
                pass: '666'
            },
            {
                name: 'gibs',
                pass: '0000'
            }
        ],
        status_array: [ 'success', 'error', 'warning', 'info' ],
    }
 },
    computed:{
        numbers(){
            let numbers = [ this.num1, this.num2, this.num3 ];

            numbers.sort(function(a, b) {
                return a - b;
            });

           return numbers;
        }
    },
    watch:{
      time(){
          if( this.time >  '17:00' ){
              this.$swal( 'Добрый вечер', '', 'success' );
          }else{
              this.$swal( 'Добрый день', '', 'success' );
          }
      }
    },
    methods:{
        validate(){
            let _this = this;

            let result = this.users.some( function( element ) {

                if ( element.name === _this.inputData.name && element.pass === _this.inputData.pass ) {
                    return true;
                }

                return false;
            });

            return result
        },

        login(){
            if( this.validate() ){
                this.$swal( 'Добро пожаловать', '' , 'success' );
            }else{
                this.$swal( 'Пользователь не найден', '' , 'error' );
            }
        }
  }
}
</script>
