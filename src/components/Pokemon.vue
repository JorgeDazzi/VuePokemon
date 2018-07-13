<template>

    <div class="gameboy" v-if="gameboy">

        <div class="screenFrame">

            <div class="screen">

                <div class="pokemon" v-bind:style="{ backgroundImage: 'url(' + img.pokePic + ')' }">
                    <p>{{ pokemons[position].ename }}</p>
                </div>

                <div class="info">
                    <ul>
                        <li>{{ pokemons[position].cname }} | {{ pokemons[position].jname }}</li>
                        <li>#{{ pokemons[position].id }}</li>
                        <li><span>Stats:</span></li>
                        <li v-for="(stat, title) in pokemons[position].base"><label>{{ title }}</label> {{ stat }}</li>
                        <li><span>Type:</span></li>
                        <li v-for="type in pokemons[position].type" class="j-30">{{elementType(type)}}</li>
                    </ul>
                </div>

            </div>

            <h2 v-on:click="next()">{{title}}</h2>

        </div>


            <div class="pause"></div>
            <div class="pause"></div>



    </div>


</template>

<script>


export default {
    name: 'Pokemon',
    data(){
      return{
          title: 'Game Boy',
          url:'https://raw.githubusercontent.com/fanzeyi/Pokemon-DB/master/pokedex.json',
          pokemons: null,
          img:{
              url:'https://raw.githubusercontent.com/fanzeyi/Pokemon-DB/master/img/',
              pokePic:''
          },
          position: 0,
          gameboy: false

      }
    },

    methods: {
        next: function ()  {
            if(this.position < this.pokemons.length) {
                this.position++;
                this.getImgUrl();
            }
        },
        previous: function () {

          if(this.position > 0) {
              this.position--;
              this.getImgUrl();
          }
        },
        getImgUrl: function(){
            this.img.pokePic = this.img.url + this.pokemons[this.position].id + this.pokemons[this.position].ename + '.png';
            this.img.pokePic = this.img.pokePic.replace('♂','');
            this.img.pokePic = this.img.pokePic.replace('♀','');
            this.img.pokePic = this.img.pokePic.replace('. ','_');
        },

        arrowKeyMagic: function (event) {

            event.key == 'ArrowUp' || event.key == 'ArrowRight' ? this.next() : this.previous();

        },

        elementType: function (element) {

            switch (element){
                case '一般' : //Normal
                    return "\u2205";
                    break;

                case '格斗' : //Fighting
                    return "\u2694";
                    break;

                case '飞行' : //Flying
                    return "\uD83E\uDD8B";
                    break;

                case '毒' : //Poison
                    return "\u2623";
                    break;

                case '地上' : //Ground
                    return "\u23DA";
                    break;

                case '岩石' : //Rock
                    return "\uD83D\uDF19";
                    break;

                case '虫' : //Bug
                    return "\uD83D\uDC1B";
                    break;

                case '幽灵' : //Ghost
                    return "\uD83D\uDC7B";
                    break;

                case '钢' : //Steel
                    return "\uD83D\uDF1B";
                    break;

                case '炎' : //Fire
                    return "\uD83D\uDD25";
                    break;

                case '水' : //Water
                    return "\uD83C\uDF0A";
                    break;

                case '草' : //Grass
                    return "\uD83C\uDF32";
                    break;

                case '电' : //
                    return "\u2301";
                    break;

                case '超能' : //Psychic
                    return "\uD83E\uDDE0";
                    break;

                case '冰' : //Ice
                    return 	"\u26C4";
                    break;

                case '龙' : //Dragon
                    return "\uD83D\uDC09";
                    break;

                case '恶' : //Dark
                    return "\uD83C\uDF11";
                    break;

                case '妖精' : //Fairy
                    return "\uD83E\uDDDA";
                    break;

                default:
                    return "\uD83C\uDF7A";



            }

        },

        randomId: function () {
                return Math.floor( 1 + Math.random() * (this.pokemons.length + 1 - 1) )
        }

    },

    mounted: async function getPokemonDB () {
        let res = await fetch(this.url, {
            method: 'GET',
        });

        let data = await res.json();
        this.pokemons = data;

        this.position = this.randomId();
        this.getImgUrl();

        this.gameboy = true;
    },

    created: function () {
        window.addEventListener('keyup', this.arrowKeyMagic)
    },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>


    .gameboy{
        position: relative;
        width: 600px;
        height: 800px;
        background: rgba(184,184,184,1);
        background-size: 100% 100%;
        border-radius: 15px 15px 60px 15px;
        box-shadow: 0 15px 6px -8px rgba(0,0,0,0.55);
        left: 50%;
        top: 50%;
        transform: translate(-50%,8%);
        border:1px solid #8b8b8b;
        z-index: 1;
    }
    .gameboy .screenFrame{
        position: absolute;
        top: 40px;
        left: 50px;
        border-radius: 14px 14px 40px 14px;
        height: 450px;
        width: 500px;
        background: #424348;
        z-index: 2;
    }
    .gameboy .screenFrame h2{
        position: absolute;
        bottom: 0;
        margin: 0 auto;
        color: #fff;
        width: 100%;
        text-align: center;
        padding: 10px 0;

    }
    .gameboy .screenFrame .screen {
        position: absolute;
        top: 10px;
        left: 10px;
        height: 400px;
        width: 480px;
        /*background: rgba(63,63,63,0.992);*/
        background: #4f5055;
        border-radius: 14px;
        z-index: 3;

    }
    .gameboy .screenFrame .screen .pokemon{
        position: absolute;
        top: 0;
        left: 0;
        height: 400px;
        width: 280px;
        border-top-left-radius: 14px;
        border-bottom-left-radius: 14px;
        background-size: 90%;
        background-repeat: no-repeat;
        background-position-x: 5px;
        background-position-y: 20px;
    }
    .gameboy .screenFrame .screen .pokemon p{
        position: absolute;
        bottom: 5px;
        width: 280px;
        text-align: center;
        color: #fff;
        font-size: 18px;
        font-weight: 300;
        letter-spacing: 2px;
        text-shadow: #000 1px 1px;
    }

    .gameboy .screenFrame .screen .info {
        position: absolute;
        top: 0;
        right: 10px;
        height: 400px;
        width: 200px;
        border-top-right-radius: 14px;
        border-bottom-right-radius: 14px;
    }
    .gameboy .screenFrame .screen .info ul{
        width: 200px;
        display: inline-block;table-layout: fixed;
        list-style: none;
        color: #fff;
        margin-top: 20px;
        background: rgba(255,255,255,0.1);
        border-radius: 14px;
        padding: 4px;
    }
    .gameboy .screenFrame .screen .info ul li,
    .gameboy .screenFrame .screen .info ul li span,
    .gameboy .screenFrame .screen .info ul li label{
        font-family: Arial;
        text-align: center;
        letter-spacing: 2px;
        font-size: 14px;
    }
    .gameboy .screenFrame .screen .info ul li{
         margin-bottom: 10px;
    }
    .gameboy .screenFrame .screen .info ul li.j-30{
        font-size: 30px;
    }

    .gameboy .pause{
        position: absolute;
        bottom: 70px;
        height: 60px;
        width: 15px;
        background: rgba(63,63,63,1);
        border-radius: 50%;
        left: 240px;
        transform: rotate(90deg);
        box-shadow: 2px 0px 2px 2px rgba(0,0,0,0.55);
    }
    .gameboy .pause:nth-child(2) {
        left: 340px;
    }

</style>
