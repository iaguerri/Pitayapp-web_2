<script setup>
import { RouterLink } from "vue-router";
import { ref } from "vue";

const is_expanded = ref(localStorage.getItem("is_expanded") === "true");
const ToggleMenu = () => {
  is_expanded.value = !is_expanded.value;
  localStorage.setItem("is_expanded", is_expanded.value);
};
</script>

<template>
  <aside :class="`${is_expanded ? 'is-expanded' : ''}`">
    <div class="top-elements">
      <button class="menu-icon" @click="ToggleMenu">
        <img src="../assets/svg/menu-icon.svg" alt="" class="menu" />
        <img src="../assets/svg/close-icon.svg" alt="" class="close" />
        <h2 class="toggle-title">Menú</h2>
      </button>
    </div>
    <div class="nav-icons">
      <RouterLink class="router-link" to="/home"
        ><button>
          <img class="view-icon" src="../assets/svg/home-iconn.svg" alt="" />
        </button>
        <h2>Home</h2>
      </RouterLink>
      <RouterLink to="/discover"
        ><button>
          <img
            class="view-icon"
            src="../assets/svg/discover-iconn.svg"
            alt=""
          />
          <div class="svg"></div>
        </button>
        <h2>Discover</h2>
      </RouterLink>
      <RouterLink to="/upload"
        ><button>
          <img class="view-icon" src="../assets/svg/upload-iconn.svg" alt="" />
        </button>
        <h2>Upload</h2>
      </RouterLink>
      <RouterLink to="/collections"
        ><button>
          <img
            class="view-icon"
            src="../assets/svg/collections-iconn.svg"
            alt=""
          />
        </button>
        <h2>Collections</h2>
      </RouterLink>
      <RouterLink class="profile-btn" to="/profile"
        ><button>
          <img
            class="view-icon not-desktop"
            src="../assets/svg/user-icon2.svg"
            alt=""
          />
        </button>
      </RouterLink>
    </div>

    <div class="pitayapp-logo">
      <img src="../assets/img/pitayapp-white-iso.png" alt="" class="loguito" />
    </div>
  </aside>
</template>

<style lang="scss" scoped>
@media (min-width: 300px) {
  aside {
    position: fixed;
    bottom: 0;
    width: 100%;
    height: 8%;
    background-color: var(--secondary);
    -webkit-box-shadow: 1px -4px 16px 8px rgba(0, 0, 0, 0.28);
    box-shadow: 1px -4px 16px 8px rgba(0, 0, 0, 0.28);
    z-index: 1;
    border-radius: 20px 20px 0 0;

    .top-elements {
      .menu-icon {
        display: none;

        .menu {
          cursor: pointer;
        }
        .close {
          display: none;
        }

        .toggle-title {
          display: none;
          background-color: transparent;
        }
      }
    }

    .nav-icons {
      background-color: transparent;
      display: flex;
      justify-content: center;
      align-items: center;
      justify-content: space-between;
      margin-top: 0;
      width: 100%;
      height: 100%;
      transition: 0.3s ease-in-out;

      & a {
        background-color: transparent;
        text-decoration: none;
        display: flex;
        align-items: center;
        justify-content: center;
        width: 100%;
        transition: 0.3s ease-in-out;

        .active {
          filter: brightness(0) saturate(100%) invert(43%) sepia(64%)
            saturate(2217%) hue-rotate(308deg) brightness(95%) contrast(105%);
        }

        &:hover {
          background-color: none;
          transition: 0.3s all;
          z-index: 1;
          width: 100%;
        }

        h2 {
          display: none;
        }

        button {
          background-color: transparent;
          outline: none;
          border: none;
          justify-content: center;

          .view-icon {
            background-color: transparent;
            width: 2rem;
            height: 2rem;
            transition: 0.2s ease-out;
            margin-top: 0.5rem;
            filter: brightness(0) saturate(100%) invert(13%) sepia(61%)
              saturate(20%) hue-rotate(38deg) brightness(102%) contrast(96%);
          }
        }
      }
    }

    .pitayapp-logo {
      .loguito {
        display: none;
      }
    }
  }

  .is-expanded {
    .top-elements {
      .menu-icon {
        img {
          margin-right: 1rem;
        }
      }
    }

    .nav-icons {
      a {
        button {
          img {
            margin-left: 1rem;
          }
        }
      }
    }
  }
}

@media (min-width: 800px) {
  #app {
    display: flex;

    aside {
      //position: fixed;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      background-color: var(--primary);
      width: calc(5rem + 1.5rem);
      height: 100%;
      overflow: hidden;
      padding: 1rem;
      transition: 0.5s ease-out;
      color: var(--secondary);
      -webkit-box-shadow: none;
      box-shadow: none;
      border-radius: 0;
      z-index: 2;

      .top-elements {
        display: flex;
        flex-direction: column;
        background-color: var(--primary);
        justify-content: center;
        transition: 0.3s ease-in-out;

        .menu-icon {
          background-color: var(--primary);
          display: flex;
          justify-content: center;
          padding: 1rem;
          outline: none;
          border: none;
          transition: 0.3s ease-out;

          .menu {
            background-color: var(--primary);
            width: 2.5rem;
            cursor: pointer;
          }
          .close {
            display: none;
            width: 2.5rem;
            cursor: pointer;
            animation: fade2 1s linear;
          }
          @keyframes fade1 {
            0% {
              opacity: 0;
            }
            100% {
              opacity: 1;
            }
          }

          @keyframes fade2 {
            0% {
              opacity: 0;
            }

            100% {
              opacity: 1;
            }
          }

          .toggle-title {
            display: none;
            background-color: transparent;
          }
        }
      }

      .nav-icons {
        background-color: transparent;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        margin-top: 1rem;
        width: 100%;
        transition: 0.3s ease-in-out;

        & a {
          background-color: transparent;
          text-decoration: none;
          display: flex;
          align-items: center;
          justify-content: center;
          width: 100%;
          transition: 0.3s ease-in-out;

          &.active.router-link-exact-active {
            background-color: var(--cursor-color);
            border-radius: 10px;
          }

          &:hover {
            z-index: 1;
            width: 100%;
            border-radius: 10px;
            background-color: var(--dope);
          }

          & h2 {
            background-color: transparent;
            text-decoration: none;
            display: none;
          }

          button {
            background-color: transparent;
            outline: none;
            border: none;
            justify-content: center;
            margin-top: 1.5rem;
            margin-bottom: 1.5rem;

            .view-icon {
              background-color: transparent;
              width: 3rem;
              transition: 0.2s ease-out;
              filter: none;
            }

            & .not-desktop {
              display: none;
            }
          }
        }

        & .profile-btn {
          display: none;
        }

        .pitayapp-logo {
          display: none;
        }

        .profile-link {
          display: none;
        }

        .pitayapp-logo {
          display: none;
        }
      }

      &.is-expanded {
        width: var(--sidebar-width);

        .top-elements {
          .toggle-title {
            display: block;
            background-color: transparent;
            color: var(--secondary);
            font-size: 1.5rem;
            transition: 0.3s ease-in-out;
            margin-left: 10px;
          }
          .menu {
            display: none;
          }

          .close {
            display: block;
            width: 2rem;
            cursor: pointer;
            transition: 0.3s ease-in-out;
          }
        }

        a {
          width: 100%;
          justify-content: flex-start;

          .nav-icons {
            background-color: transparent;
            margin-right: 1rem;
          }

          & h2 {
            background-color: transparent;
            color: var(--secondary);
            font-size: 1.5rem;
            font-weight: 700;
            text-decoration: none;
            margin-left: 20px;
            transition: 0.3s ease-in-out;
            display: block;
          }
        }

        .pitayapp-logo {
          display: flex;
          align-items: center;
          justify-content: center;

          .loguito {
            width: 5rem;
            height: 5rem;
            display: block;
          }
        }
      }
    }
  }
}
</style>
