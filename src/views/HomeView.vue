<script setup>
/* borrar, copiar img a public (public/recipes) cambiar la ur
linea 16, 19, 22 (url) -> poner la ruta con este formato: 
"recipes/hamburguesa_lentejas_tofu.jpg"
*/
import { ref } from "vue";
import croquetasTofuImage from "../assets/recipes/croquetas_tofu.jpg";
import hamburguesaLentejasImage from "../assets/recipes/hamburguesa_lentejas_tofu.jpg";
import clafoutisFrambuesaImage from "../assets/recipes/clafoutis-frambuesa.jpg";
import { useUserStore } from "../stores/userStore";
import { RouterLink } from "vue-router";
import { Icon } from "@iconify/vue";
import SearcherBar from "@/components/SearcherBar.vue";

const userStore = useUserStore();

/* const username = ref(""); */
const mostPopular = ref([{id: "/recipes/9", title: "Croquetas de tofu", url: croquetasTofuImage}, {id: "/recipes/17", title: "Hamburguesa de lenteja y tofu", url: hamburguesaLentejasImage}, {id: "/recipes/31", title: "Clafoutis de frambuesa", url: clafoutisFrambuesaImage}]);

const goOut = async () => {
  userStore.logOut();
};

/* export default {
  name: "HomeView",

  data() {
    return {
      username: "",
      mostPopular: [
        {
          id: "/recipes/9",
          title: "Croquetas de tofu",
          url: croquetasTofuImage,
        },
        {
          id: "/recipes/17",
          title: "Hamburguesa de lenteja y tofu",
          url: hamburguesaLentejasImage,
        },
        {
          id: "/recipes/31",
          title: "Clafoutis de frambuesa",
          url: clafoutisFrambuesaImage,
        },
      ],
    };
  },

  methods: {
    goOut() {
      userStore.logOut();
    }
  }

}; */
</script>

<template>
  <main class="home-view">
    <div class="container">
      <div class="top-container">
        <div class="hello">
          <p>
            <Icon 
              icon="noto-v1:victory-hand"
              color="#f9458e"
              height="25"
              :rotate="2"
              :horizontalFlip="true"
              :verticalFlip="true"
            />
            Hola Pitayapper <!-- {{ username }} -->!
          </p>
          <a @click="goOut"><img src="../assets/svg/logout-icon.svg" alt="" class="logout-icon" /></a>
        </div>
        <SearcherBar class="searcher-comp mobile" />
      </div>
      <div class="content">
        <div class="left-container">
          <div class="most-popular">
            <div class="most-popular-text">
              <h2>Más populares</h2>
              <RouterLink to="/discover" class="seeMore">Ver más</RouterLink>
              <!-- <a href="">Ver más</a> -->
            </div>
            <div class="recipe-list">
              <div
                v-for="(recipe, i) in mostPopular"
                :key="i"
                class="popular-recipes"
              >
                <img :src="recipe.url" />
                <h4 class="title">{{ recipe.title }}</h4>
                <RouterLink :to="recipe.id">
                  <button>Ver</button>
                </RouterLink>
              </div>
            </div>
          </div>
          <div class="bottom-container">
            <div class="categories">
              <div class="categorie-container week">
                <div class="transparent">
                  <h3 class="title">Recetas de la semana</h3>
                </div>
              </div>
            </div>
            <div class="categories">
              <div class="categorie-container family">
                <div class="transparent">
                  <h3 class="title">Para cenar en familia</h3>
                </div>
              </div>
            </div>
            <div class="categories">
              <div class="categorie-container diet">
                <div class="transparent">
                  <h3 class="title">Comenzando la dieta</h3>
                </div>
              </div>
            </div>
            <div class="categories">
              <div class="categorie-container children">
                <div class="transparent">
                  <h3 class="title">Para los más peques</h3>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="right-container">
          <SearcherBar class="searcher-comp desktop" />
          <div class="your-recipes">
            <p>Tus Recetas</p>
            <div class="user-recipes">
              <div
                v-for="(recipe, i) in mostPopular"
                :key="i"
                class="popular-recipes"
              >
                <RouterLink :to="recipe.id">
                  <h4 class="title">{{ recipe.title }}</h4>
                </RouterLink>
              </div>
            </div>
          </div>
          <div class="buttons">
            <!-- <button>Mis colecciones</button> -->
            <RouterLink to="/collections">Mis colecciones</RouterLink>
            <RouterLink to="/upload">Crear nueva receta</RouterLink>
            <!-- <button>Crear nueva receta</button> -->
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<style lang="scss" scoped>
body {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  width: 100vw;
  height: 100vh;
  transition: 0.5s ease-out;

  .home-view {
    width: 100vw;
    height: 100vh;
    margin-bottom: 6rem;

    & .container {
      display: flex;
      flex-direction: column;

      & .top-container {
        background-color: #f9458e;
        color: white;
        width: 100%;
        height: 20%;
        border-radius: 0 0 15px 15px;
        display: flex;
        flex-direction: column;
        padding: 5% 12% 5% 12%;
        box-sizing: border-box;
        justify-content: space-evenly;

        & .hello {
          display: flex;
          justify-content: space-between;
          align-items: center;
          background-color: transparent;
          height: 3rem;
          margin-right: 0.5rem;

          & p {
            display: flex;
            justify-content: center;
            align-items: center;
            background-color: transparent;
            height: auto;
            width: auto;
            font-weight: bold;
            font-size: 1.2rem;
            padding: 0rem 0.1rem;
          }

          .logout-icon {
            background-color: transparent;
            cursor: pointer;
            height: 1.2rem;
            filter: brightness(0) saturate(100%) invert(100%) sepia(0%)
              saturate(6795%) hue-rotate(235deg) brightness(121%) contrast(100%);
          }
        }

        .mobile {
          height: 2rem;
        }
      }

      & .right-container {
        display: none;
      }

      .most-popular {
        width: 100%;
        height: 33%;

        & .most-popular-text {
          margin-top: 1rem;
          padding: 0 1.5rem 0 1.2rem;
          box-sizing: border-box;
          width: 100%;
          height: 20%;
          display: flex;
          justify-content: space-between;
          align-items: center;

          a{
            text-decoration: none;
            background: #f9458e;
            padding: 0.4rem;
            border-radius: 0.5rem;
            color: white;
            transition: all 1s;
          }
          a:hover{
            background: #b83268;
            transition: all 1s;
          }

          &p {
            cursor: pointer;
          }
        }

        & .recipe-list {
          width: 100%;
          height: 100%;
          display: flex;
          justify-content: center;

          & .popular-recipes {
            margin: 1rem 0.5rem;
            height: 9rem;
            width: 7rem;
            box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.28);
            border-radius: 15px;
            display: grid;
            grid-template-rows: 60% 20% 20%;
            place-items: center;
            cursor: pointer;

            & img {
              max-width: 90%;
              max-height: 80%;
            }

            & h4 {
              width: 90%;
              text-align: center;
              font-size: 0.7rem;
            }

            & button {
              background-color: #f9458e;
              color: white;
              border-radius: 15px;
              border: none;
              height: 1.2rem;
              width: 2.5rem;
              cursor: pointer;
            }
          }
        }
      }

      .bottom-container {
        height: 47%;
        margin: 1rem 0 6rem 0;

        .categories {
          width: 100%;
          height: 8rem;
          display: flex;
          justify-content: center;
          align-items: center;
          cursor: pointer;

          & .categorie-container {
            width: 80%;
            height: 7rem;
            display: flex;
            align-items: center;
            justify-content: center;
            box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.28);
            border-radius: 15px;
            /* background: rgba(151, 151, 151, 0.57); */
            background-position: center;
            background-size: 100%;

            & .transparent {
              width: 100%;
              height: 100%;
              background: rgba(151, 151, 151, 0.57);
              display: flex;
              align-items: center;
              justify-content: center;
              border-radius: 15px;
            }
          }

          & .week {
            background-image: url("../assets/img/recetasdelasemana.jpg");
          }

          & .family {
            background-image: url("../assets/img/paracenarenfamilia.jpg");
          }

          & .diet {
            background-image: url("../assets/img/comenzandoladieta.jpg");
          }

          & .children {
            background-image: url("../assets/img/paralospeques.jpg");
          }

          & h3 {
            background: transparent;
            color: white;
          }
        }
      }
    }
  }
}

@media (min-width: 800px) {
  body {
    width: 100vw;
    height: 100vh;

    & .home-view {
      margin-bottom: 0;
      box-sizing: border-box;

      & .container {
        height: 90%;
        width: 94%;
        position: absolute;
        top: 5.5rem;
        left: 6.5rem;
        padding: 2rem;
        box-sizing: border-box;

        & .top-container {
          background-color: transparent;
          color: black;
          height: 5%;
          border-radius: 0;
          display: flex;
          flex-direction: column;
          padding: 0;
          justify-content: center;

          & .hello {
            & svg {
              margin-right: 0.2rem;
              height: 1.95rem;
              width: 1.95rem;
            }

            & p {
              font-size: 1.6rem;
            }

            .logout-icon {
              display: none;
            }
          }

          & .mobile {
            display: none;
          }
        }

        & .content {
          height: 100%;
          width: 100%;
          margin-top: 0;
          display: grid;
          grid-template-columns: 50% 50%;

          & .left-container {
            height: 100%;
            width: 100%;
            display: flex;
            flex-direction: column;
            justify-content: space-around;

            .most-popular {
              width: 100%;
              height: 40%;
              display: flex;
              flex-direction: column;
              align-items: center;
              margin-top: 2.5%;

              & .most-popular-text {
                margin-top: 0;
                font-size: 0.8rem;
                height: 20%;

                a{
                  background: #f9458e;
                  padding: 0.5rem;
                  border-radius: 0.5rem;
                  color: white;
                  transition: all 1s;
                }
                a:hover{
                  background: #b83268;
                  transition: all 1s;
                }
              }

              & .recipe-list {
                width: 100%;
                height: 100%;
                display: flex;
                justify-content: center;

                & .popular-recipes {
                  margin: 1rem 0.5rem;
                  height: 9rem;
                  width: 7rem;
                  box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.28);
                  border-radius: 15px;
                  display: grid;
                  grid-template-rows: 60% 20% 20%;
                  place-items: center;
                  cursor: pointer;

                  & img {
                    max-width: 90%;
                    max-height: 80%;
                  }

                  & h4 {
                    width: 90%;
                    text-align: center;
                    font-size: 0.7rem;
                  }

                  & button {
                    background-color: #f9458e;
                    color: white;
                    border-radius: 0.6rem;
                    border: none;
                    height: 1.2rem;
                    width: 2.5rem;
                    transition: all 1s;
                  }

                  button:hover{
                    background: #b83268;
                    transition: all 1s;
                  }
                }
              }

              & .recipe-list {
                width: 100%;
                height: 80%;
                display: flex;
                justify-content: space-around;

                & .popular-recipes {
                  height: 100%;
                  width: 30%;
                  display: flex;
                  flex-direction: column;
                  justify-content: space-evenly;
                  align-items: center;

                  & img {
                    max-width: 90%;
                    max-height: 50%;
                  }

                  & h4 {
                    width: 90%;
                    text-align: center;
                    font-size: 100%;
                  }

                  & button {
                    height: 2rem;
                    width: 3.5rem;
                  }
                }
              }
            }

            .bottom-container {
              height: 50%;
              width: 100%;
              margin: 2.5% 0 0 0;
              display: grid;
              grid-template-columns: 50% 50%;
              grid-template-rows: 50% 50%;

              .categories {
                width: 100%;
                height: 100%;

                & .categorie-container {
                  width: 95%;
                  height: 75%;
                  display: flex;
                  align-items: center;
                  justify-content: center;
                  box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.28);
                  border-radius: 15px;
                  background-position: center;
                  background-size: 100%;
                }
              }
            }
          }

          & .right-container {
            width: 100%;
            height: 90%;
            display: grid;
            grid-template-rows: 7% 70% 7%;
            grid-row-gap: 3%;
            align-content: end;
            justify-items: center;

            & .searcher-comp {
              width: 70%;
            }

            & .your-recipes {
              width: 70%;
              box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.28);
              border-radius: 15px;
              padding: 1rem;
              box-sizing: border-box;

              & p {
                font-size: 1.5rem;
                font-weight: bold;
              }

              & .user-recipes {
                height: 80%;
                display: grid;
                grid-template-rows: 30% 30% 30%;
                grid-row-gap: 8%;

                & .popular-recipes {
                  margin: 1rem;
                  height: 100%;
                  width: 90%;
                  box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.28);
                  border-radius: 15px;
                  display: flex;
                  align-items: center;
                  justify-content: center;
                  cursor: pointer;
                }
              }
            }

            & .buttons {
              width: 70%;
              display: flex;
              justify-content: space-around;

              & a {
                width: 40%;
                height: 100%;
                background: #f9458e;
                border: 0;
                box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.28);
                border-radius: 10px;
                font-family: "Inter";
                font-style: normal;
                font-weight: 700;
                font-size: 1rem;
                color: white;
                cursor: pointer;
                display: flex;
                justify-content: center;
                align-items: center;
                text-decoration: none;
              }
            }
          }
        }
      }
    }
  }
}

.route-center-from {
  opacity: 0;
  transform: translateX(50px);
}

.route-enter-active {
  transition: all 0.4s ease-in;
}

.route-leave-to {
  opacity: 0;
  transform: translateX(-50px);
}

.route-leave-active {
  transition: all 0.4s ease-out;
}
</style>
