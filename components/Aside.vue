<template>
  <div>
    <ul class="menu">
      <li
        v-for="(menuItem, mindex) in Menus"
        class="menu-item"
        :class="{ activeted: menuItem.activeted }"
        :key="mindex"
      >
        <span class="menu-title">{{ menuItem.title }}</span>
        <template v-if="menuItem.children.length">
          <ul class="submenu">
            <li
              v-for="(subMenuItem, sindex) in menuItem.children"
              class="submenu-item"
              :class="{ subactiveted: subMenuItem.activeted }"
              :key="sindex"
            >
              <span class="submenu-title">{{ subMenuItem.title }}</span>
            </li>
          </ul>
        </template>
      </li>
    </ul>
  </div>
</template>

<script>
const Menus = [
  {
    id: "0",
    title: "My Profile",
    activeted: false,
    children: [],
  },
  {
    id: "1",
    title: "Address Book",
    activeted: false,
    children: [],
  },
  {
    id: "2",
    title: "Booking History",
    activeted: true,
    children: [
      {
        id: "2-1",
        title: "Upcoming",
        activeted: true,
        children: [],
      },
      {
        id: "2-2",
        title: "Completed",
        activeted: false,
        children: [],
      },
      {
        id: "2-3",
        title: "Canceled",
        activeted: false,
        children: [],
      },
    ],
  },
  {
    id: "3",
    title: "Payments Details",
    activeted: false,
    children: [],
  },
  {
    id: "4",
    title: "Update Password",
    activeted: false,
    children: [],
  },
  {
    id: "5",
    title: "Log in",
    activeted: false,
    children: [],
  },
  {
    id: "6",
    title: "Log out",
    activeted: false,
    children: [],
  },
];
export default {
  data() {
    return {
      Menus,
    };
  },
};
</script>

<style lang="scss" scope>
$theme-color: #ec7211;

ul {
  list-style: none;
}
.menu {
  .menu-item {
    padding: 10px 0;
    cursor: pointer;
    span {
      font-size: 20px;
    }

    .submenu {
      position: relative;
      margin-left: 10px;
      padding-left: 0;

      .submenu-item {
        padding: 10px 0;
        padding-left: 20px;
      }
    }
    &.activeted {
      .menu-title {
        color: $theme-color;
      }
      .submenu {
        &::before {
          position: absolute;
          left: 0;
          top: 50%;
          display: inline-block;
          content: "";
          width: 2px;
          height: 80%;
          transform: translateX(-50%) translateY(-50%);
          background: $theme-color;
        }
        .subactiveted {
          color: $theme-color;
        }
      }
    }
  }
}
</style>