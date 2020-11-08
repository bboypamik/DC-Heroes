<template>
    <div id="app">
        <img id="logo" alt="DC HEROES" src="./assets/dc_heroes_logo.png">
        <h2>DC Heroes count: {{heroesCount}}</h2>
        <div class="hero-list">
            <ul>
                <li  v-for="(hero,index) in state.dcHeroes" :key="hero.name">
                    <div>{{hero.name}} <button @click="deleteHero(index)">x</button></div>
                </li>
            </ul>
        </div>
        <div class="add-hero">
            <form @submit.prevent="addHero">
                <input v-model="state.newHero" placeholder="Heroin" />
                <button>Add Hero</button>
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
