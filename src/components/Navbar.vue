<script>
import { defineComponent } from "vue";
import { library } from "@fortawesome/fontawesome-svg-core";
import {
  faUser,
  faRightFromBracket,
  faPlus,
  faList,
} from "@fortawesome/free-solid-svg-icons";
library.add(faUser, faRightFromBracket, faPlus, faList);
export default defineComponent({
  name: "Navbar",
  computed: {
    obtenerRol() {
      return localStorage.getItem("rol");
    },
    getMainPage() {
      if (this.obtenerRol == "CLIENTE") {
        return "/misperfilesusuario";
      } else if (this.obtenerRol == "ADMINISTRADOR") {
        return "/solicitudesadministrador";
      } else if (this.obtenerRol == null) {
        return "/";
      }
    },
  },
  methods: {
    cerrarSesion() {
      localStorage.removeItem("token");
      localStorage.removeItem("rol");
    },
  },
});
</script>
<template>
  <header class="position-sticky top-0 left-0 z-index-3 p-0">
    <nav class="navbar navbar-expand-lg navbar-dark">
      <div class="container-fluid py-3 px-4">
        <router-link
          :to="getMainPage"
          class="navbar-brand my-0 me-0 p-0 ms-md-3 ms-lg-5"
        >
          <img
            src="../assets/images/zorrito-icon.svg"
            alt="Ícono de Zorrito Plus"
            class="logo-icon"
        /></router-link>
        <button
          class="navbar-toggler collapsed d-flex d-lg-none flex-column justify-content-around ms-0 me-md-3 me-lg-5 p-0 border-0 position-relative"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#navbarNav"
          aria-controls="navbarNav"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span
            class="navbar-toggler__icon navbar-toggler__icon--top-bar"
          ></span>
          <span
            class="navbar-toggler__icon navbar-toggler__icon--middle-bar"
          ></span>
          <span
            class="navbar-toggler__icon navbar-toggler__icon--bottom-bar"
          ></span>
        </button>
        <div
          class="collapse navbar-collapse justify-content-end my-0 mx-0 p-0 mx-md-3 ms-lg-0 me-lg-5"
          id="navbarNav"
        >
          <ul class="navbar-nav d-lg-flex align-items-center pt-4 pt-lg-0">
            <template v-if="obtenerRol == 'CLIENTE'">
              <li
                class="nav-item dropdown pb-2 py-lg-0 px-0 pe-lg-4 text-center"
              >
                <div
                  id="perfilesButton"
                  class="nav-link active dropdown-toggle fs-5 p-0 fw-bold text-uppercase readex-pro text-break"
                  role="button"
                  data-bs-toggle="dropdown"
                  aria-expanded="false"
                >
                  Perfiles
                </div>
                <ul class="dropdown-menu dropdown-menu-dark mt-2 border-0">
                  <li>
                    <router-link
                      to="/misperfilesusuario"
                      class="dropdown-item fs-5 text-white text-break"
                      ><font-awesome-icon
                        icon="fa-solid fa-list"
                        class="pe-2"
                      />Mis perfiles</router-link
                    >
                  </li>
                  <li><hr class="dropdown-divider" /></li>
                  <li>
                    <router-link
                      to="/solicitarperfilusuario"
                      id="solicitarPerfilButton"
                      class="dropdown-item fs-5 text-white text-break"
                      ><font-awesome-icon
                        icon="fa-solid fa-plus"
                        class="pe-2"
                      />Solicitar perfil</router-link
                    >
                  </li>
                  <li><hr class="dropdown-divider" /></li>
                  <li>
                    <router-link
                      to="/missolicitudesusuario"
                      class="dropdown-item fs-5 text-white text-break"
                      ><font-awesome-icon
                        icon="fa-solid fa-list"
                        class="pe-2"
                      />Mis solicitudes</router-link
                    >
                  </li>
                </ul>
              </li>
              <li
                class="nav-item dropdown py-2 py-lg-0 px-0 px-lg-4 text-center"
              >
                <div
                  class="nav-link active dropdown-toggle fs-5 p-0 fw-bold text-uppercase readex-pro text-break"
                  role="button"
                  data-bs-toggle="dropdown"
                  aria-expanded="false"
                >
                  Quejas
                </div>
                <ul class="dropdown-menu dropdown-menu-dark mt-2 border-0">
                  <li>
                    <router-link
                      to="/misquejasusuario"
                      class="dropdown-item fs-5 text-white text-break"
                      ><font-awesome-icon
                        icon="fa-solid fa-list"
                        class="pe-2"
                      />Mis quejas</router-link
                    >
                  </li>
                  <li><hr class="dropdown-divider" /></li>
                  <li>
                    <router-link
                      to="/ingresarquejausuario"
                      class="dropdown-item fs-5 text-white text-break"
                      ><font-awesome-icon
                        icon="fa-solid fa-plus"
                        class="pe-2"
                      />Ingresar queja</router-link
                    >
                  </li>
                </ul>
              </li>
              <li
                class="nav-item dropdown pt-2 py-lg-0 px-0 ps-lg-4 text-center"
              >
                <div
                  id="miCuentaButton"
                  class="nav-link active dropdown-toggle fs-5 p-0 fw-bold text-uppercase readex-pro text-break"
                  role="button"
                  data-bs-toggle="dropdown"
                  aria-expanded="false"
                >
                  Mi cuenta
                </div>
                <ul class="dropdown-menu dropdown-menu-dark mt-2 border-0">
                  <li>
                    <router-link
                      to="/miinformacionusuario"
                      class="dropdown-item fs-5 text-white text-break"
                    >
                      <font-awesome-icon icon="fa-solid fa-user" class="pe-2" />
                      Mi información</router-link
                    >
                  </li>
                  <li><hr class="dropdown-divider" /></li>
                  <li>
                    <router-link
                      id="cerrarSesionButtonCliente"
                      to="/iniciarsesion"
                      class="dropdown-item fs-5 text-white text-break"
                      @click="cerrarSesion"
                      ><font-awesome-icon
                        icon="fa-solid fa-right-from-bracket"
                        class="pe-2"
                      />Cerrar sesión</router-link
                    >
                  </li>
                </ul>
              </li>
            </template>
            <template v-if="obtenerRol == 'ADMINISTRADOR'">
              <li
                class="nav-item dropdown pb-2 py-lg-0 px-0 pe-lg-4 text-center"
              >
                <div
                  class="nav-link active dropdown-toggle fs-5 p-0 fw-bold text-uppercase readex-pro text-break"
                  role="button"
                  data-bs-toggle="dropdown"
                  aria-expanded="false"
                >
                  Perfiles
                </div>
                <ul class="dropdown-menu dropdown-menu-dark mt-2 border-0">
                  <li>
                    <router-link
                      to="/perfilesadministrador"
                      class="dropdown-item fs-5 text-white text-break"
                      ><font-awesome-icon
                        icon="fa-solid fa-list"
                        class="pe-2"
                      />Perfiles</router-link
                    >
                  </li>
                  <li><hr class="dropdown-divider" /></li>
                  <li>
                    <router-link
                      to="/solicitudesadministrador"
                      class="dropdown-item fs-5 text-white text-break"
                      ><font-awesome-icon
                        icon="fa-solid fa-list"
                        class="pe-2"
                      />Solicitudes</router-link
                    >
                  </li>
                  <li><hr class="dropdown-divider" /></li>
                  <li>
                    <router-link
                      to="/ingresarplataformaadministrador"
                      class="dropdown-item fs-5 text-white text-break"
                      ><font-awesome-icon
                        icon="fa-solid fa-plus"
                        class="pe-2"
                      />Ingresar plataforma</router-link
                    >
                  </li>
                </ul>
              </li>
              <li class="nav-item py-2 pt-0 py-lg-0 px-0 px-lg-4">
                <router-link
                  to="/quejasadministrador"
                  class="nav-link active fs-5 p-0 fw-bold text-uppercase"
                  >Quejas</router-link
                >
              </li>
              <li class="nav-item py-2 pt-0 py-lg-0 px-0 px-lg-4">
                <router-link
                  to="/usuariosadministrador"
                  class="nav-link active fs-5 p-0 fw-bold text-uppercase"
                  >Usuarios</router-link
                >
              </li>
              <li class="nav-item pt-2 pb-0 py-lg-0 px-0 ps-lg-4">
                <router-link
                  id="cerrarSesionButtonAdmin"
                  to="/iniciarsesion"
                  class="nav-link active fs-5 p-0 fw-bold text-uppercase"
                  @click="cerrarSesion"
                >
                  <button
                    class="bg-black text-white border-white rounded-4 py-2 px-3 fw-bold text-uppercase"
                  >
                    Cerrar sesión
                    <svg
                      width="32"
                      height="35"
                      viewBox="0 0 32 35"
                      fill="none"
                      xmlns="http://www.w3.org/2000/svg"
                    >
                      <rect
                        x="9"
                        y="1"
                        width="22"
                        height="33"
                        stroke="white"
                        stroke-width="2"
                      />
                      <path
                        d="M24.0607 19.0607C24.6464 18.4749 24.6464 17.5251 24.0607 16.9393L14.5147 7.3934C13.9289 6.80761 12.9792 6.80761 12.3934 7.3934C11.8076 7.97919 11.8076 8.92893 12.3934 9.51472L20.8787 18L12.3934 26.4853C11.8076 27.0711 11.8076 28.0208 12.3934 28.6066C12.9792 29.1924 13.9289 29.1924 14.5147 28.6066L24.0607 19.0607ZM0 19.5L23 19.5V16.5L0 16.5L0 19.5Z"
                        fill="white"
                      />
                    </svg></button
                ></router-link>
              </li>
            </template>
            <template v-else-if="obtenerRol == null">
              <li class="nav-item pb-2 pt-0 py-lg-0 px-0 pe-lg-4">
                <router-link
                  to="/"
                  class="nav-link active fs-5 p-0 fw-bold text-uppercase"
                  >Inicio</router-link
                >
              </li>
              <li class="nav-item py-2 py-lg-0 px-0 px-lg-4">
                <router-link
                  to="/servicios"
                  class="nav-link active fs-5 p-0 fw-bold text-uppercase"
                  >Servicios</router-link
                >
              </li>
              <li class="nav-item pt-2 pb-0 py-lg-0 px-0 ps-lg-4">
                <router-link
                  to="/iniciarsesion"
                  class="nav-link active fs-5 p-0 fw-bold text-uppercase"
                >
                  <button
                    class="bg-black text-white border-white rounded-4 py-2 px-3 fw-bold text-uppercase"
                  >
                    Iniciar sesión
                    <svg
                      width="25"
                      height="25"
                      viewBox="0 0 30 33"
                      fill="none"
                      xmlns="http://www.w3.org/2000/svg"
                    >
                      <path
                        d="M28.7434 32H1C4.4077 24.1099 6.60302 20.0727 16.1327 20.5C23.5899 20.4179 26.3019 23.0251 28.7434 32Z"
                        stroke="white"
                      />
                      <path
                        d="M23.7035 8.5C23.7035 12.9141 20.0923 16.5 15.6283 16.5C11.1643 16.5 7.55307 12.9141 7.55307 8.5C7.55307 4.08587 11.1643 0.5 15.6283 0.5C20.0923 0.5 23.7035 4.08587 23.7035 8.5Z"
                        stroke="white"
                      />
                    </svg></button
                ></router-link>
              </li>
            </template>
          </ul>
        </div>
      </div>
    </nav>
  </header>
</template>
<style scoped lang="scss">
header {
  background-image: linear-gradient(to bottom right, black 50%, #040c51 100%);
  z-index: 3;
}
.logo-icon {
  max-width: 8rem;
}
.nav-link {
  font-family: "Readex Pro", sans-serif;
}
.navbar-toggler {
  width: 35px;
  height: 31px;
  -webkit-transition: 0.5s ease-in-out;
  -o-transition: 0.5s ease-in-out;
  transition: 0.5s ease-in-out;
  outline: none;
  -webkit-box-shadow: none;
  box-shadow: none;
  border: 0;
  &__icon {
    display: block;
    position: absolute;
    height: 5px;
    width: 100%;
    background-color: white;
    border-radius: 50px;
    opacity: 1;
    left: 0;
    -webkit-transform: rotate(0deg);
    -ms-transform: rotate(0deg);
    transform: rotate(0deg);
    -webkit-transition: 0.25s ease-in-out;
    -o-transition: 0.25s ease-in-out;
    transition: 0.25s ease-in-out;
    &--top-bar {
      margin-top: 0px;
      -webkit-transform: rotate(135deg);
      -ms-transform: rotate(135deg);
      transform: rotate(135deg);
    }
    &--middle-bar {
      opacity: 0;
      margin-top: 0px;
      filter: alpha(opacity=0);
    }
    &--bottom-bar {
      margin-top: 0px;
      -webkit-transform: rotate(-135deg);
      -ms-transform: rotate(-135deg);
      transform: rotate(-135deg);
    }
  }
  &.collapsed {
    .navbar-toggler__icon--top-bar {
      position: absolute;
      top: 0;
      right: 0;
      -webkit-transform: rotate(0deg);
      -ms-transform: rotate(0deg);
      transform: rotate(0deg);
    }
    .navbar-toggler__icon--middle-bar {
      position: absolute;
      opacity: 1;
      filter: alpha(opacity=100);
    }
    .navbar-toggler__icon--bottom-bar {
      -webkit-transform: rotate(0deg);
      -ms-transform: rotate(0deg);
      transform: rotate(0deg);
      position: absolute;
      bottom: 0;
      right: 0;
    }
  }
}
</style>
