<template>
  <nav
    class="nav"
    :class="{ open: isOpen === true }"
    aria-label="Main navigation"
  >
    <ul>
      <li>
        <router-link :to="{ name: 'Home' }">
          <div @click="handleClick">Home</div>
        </router-link>
      </li>
      <li>
        <router-link :to="{ name: 'AddProject' }">
          <div @click="handleClick">AddProject</div>
        </router-link>
      </li>
    </ul>
  </nav>
</template>

<script>
import { ref } from "vue";

export default {
  name: "Navbar",
  props: ["isOpen"],
  setup(props, context) {
    const btnIsOpen = ref(false);

    const handleClick = () => {
      //obs!!
      btnIsOpen.value = props.isOpen;
      btnIsOpen.value = !btnIsOpen.value;
      context.emit("toggleOpen", btnIsOpen.value);
    };
    return {
      btnIsOpen,
      handleClick,
    };
  },
};
</script>

<style lang="scss">
.nav {
  //position: absolute;
  height: 100%;
  position: fixed; //obs!!
  top: 0;
  left: -300px; //obs!!
  z-index: 0; //obs!!  //same parent as vego_burger
  background: $color_gray;
  height: 100%;
  width: 300px; //obs!!
  padding: 4rem;
  padding-top: 6rem;
  transition: left ease-in 0.3s; //obs!!
  text-align: left;
  a {
    color: $color_gray_dark;
    display: block;
    margin-bottom: 0.7rem;
    text-decoration: none;
    &:hover {
      color: $color_green;
      text-decoration: underline;
    }
    &.router-link-active {
      color: $color_green;
      padding-bottom: 4px;
    }
  }
  &.open {
    left: 0;
  }
}
</style>
