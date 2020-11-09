<template>
    <div id="app">
        <img id="logo" alt="DC HEROES" src="./assets/dc_heroes_logo.png">
        <h2>DC Heroes count: {{heroesCount}}</h2>
        <div  class="container hero-list">
            <ul class="list-group ">
                <li  class="list-group-item d-flex justify-content-between" v-for="(hero,index) in state.dcHeroes" :key="hero.name">
                    <div class="ml-5">{{hero.name}}</div>
                    <div><button class="btn btn-danger mr-5" @click="deleteHero(index)">x</button></div>
                </li>
            </ul>
        </div>
        <div class="add-hero mt-4">
            <form class="" @submit.prevent="addHero">
                <input v-model="state.newHero" placeholder="Heroin" />
                <button class="btn btn-primary ml-1 ">Add Hero</button>
            </form>
        </div>
    </div>
</template>

<script>
    import {reactive, computed} from 'vue';


    export default {
        name: 'App',

        setup() {

            const state = reactive({
                newHero: '',
                dcHeroes: [{
                    name: "SuperGirl"
                }
                    ,
                    {
                        name: "Flash"
                    }
                    ,
                    {
                        name: "Batman"
                    }
                    ,
                    {
                        name: "Arrow"
                    }
                    ,
                    {
                        name: "SuperMan"
                    }]
            });

            function addHero() {
              if (state.newHero) {
                  state.dcHeroes.unshift({
                      name: state.newHero
                  })
              }
                state.newHero = '';
            }
            
            function deleteHero(index) {
              state.dcHeroes = state.dcHeroes.filter((hero, i) => i !=index)
            }

          const heroesCount = computed(() => state.dcHeroes.length)


            return {
                state,
                addHero,
                heroesCount,
                deleteHero

            }
        }
    }
</script>

<style>
    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;

    }

    #logo {
        max-height: 250px;

    }
</style>
