<template>
  <ul :class="{ open: value }" class="sidenav app-sidenav">
    <router-link
        :exact="link.exact"
        :key="link.url"
        :to="link.url"
        active-class="active"
        tag="li"
        v-for="link in links"
    >
      <a class="waves-effect waves-orange pointer" href="#">{{ link.title }}</a>
    </router-link>
  </ul>
</template>

<script>
export default {
  props: ["value"],
  data: () => ({
    links: [
      {title: "Счет", url: "/", exact: true},
      {title: "История", url: "/history"},
      {title: "Планирование", url: "/planning"},
      {title: "Новая запись", url: "/record"},
      {title: "Категории", url: "/categories"}
    ]
  })
};
</script>
