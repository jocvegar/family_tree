<template>
  <div id="FamilyChart" class="f3"></div>
</template>

<script setup>
import f3 from "family-chart";
import people from "../assets/data.json";
import { onMounted } from "vue";

onMounted(() => {
  const store = f3.createStore({
      data: people,
      node_separation: 325,
      level_separation: 175,
    }),
    view = f3.d3AnimationView({
      store,
      cont: document.querySelector("#FamilyChart"),
    }),
    Card = f3.elements.Card({
      store,
      svg: view.svg,
      card_dim: {
        w: 300,
        h: 70,
        text_x: 75,
        text_y: 15,
        img_w: 60,
        img_h: 60,
        img_x: 5,
        img_y: 5,
      },
      card_display: [
        (d) => `${d.data["first name"] || ""} ${d.data["last name"] || ""}`,
        (d) => `${d.data["birthday"] || ""} ${d.data["rip"] || ""}`,
      ],
      mini_tree: true,
      link_break: false,
    });

  view.setCard(Card);
  store.setOnUpdate((props) => view.update(props || {}));
  store.update.tree({ initial: true });
});
</script>

<style>
.f3 {
  height: 100vh;
  width: 100%;
  margin: auto;
  position: relative;
}

.f3 .cursor-pointer {
  cursor: pointer;
}
.f3 svg.main_svg {
  width: 100%;
  height: 100%;
  /* background-color: #3b5560;
  color: #3b5560; */
}
.f3 svg.main_svg text {
  fill: currentColor;
}
.f3 rect.card-female,
.f3 .card-female .card-body-rect,
.f3 .card-female .text-overflow-mask {
  fill: pink;
}
.f3 rect.card-male,
.f3 .card-male .card-body-rect,
.f3 .card-male .text-overflow-mask {
  fill: lightblue;
}
.f3 .card-genderless .card-body-rect,
.f3 .card-genderless .text-overflow-mask {
  fill: lightgray;
}
.f3 .card_add .card-body-rect {
  fill: #3b5560;
  stroke-width: 4px;
  stroke: #fff;
  cursor: pointer;
}
.f3 g.card_add text {
  fill: #fff;
}
.f3 .card-main {
  stroke: #000;
}
.f3 .card_family_tree rect {
  transition: 0.3s;
}
.f3 .card_family_tree:hover rect {
  transform: scale(1.1);
}
.f3 .card_add_relative {
  cursor: pointer;
  color: #fff;
  transition: 0.3s;
}
.f3 .card_add_relative circle {
  fill: rgba(0, 0, 0, 0);
}
.f3 .card_add_relative:hover {
  color: #fff;
}
.f3 .card_edit.pencil_icon {
  color: #fff;
  transition: 0.3s;
}
.f3 .card_edit.pencil_icon:hover {
  color: #fff;
}
.f3 .card_break_link,
.f3 .link_upper,
.f3 .link_lower,
.f3 .link_particles {
  transform-origin: 50% 50%;
  transition: 1s;
}
.f3 .card_break_link {
  color: #fff;
}
.f3 .card_break_link.closed .link_upper {
  transform: translate(-140.5px, 655.6px);
}
.f3 .card_break_link.closed .link_upper g {
  transform: rotate(-58deg);
}
.f3 .card_break_link.closed .link_particles {
  transform: scale(0);
}
.f3 .input-field input {
  height: 2.5rem !important;
}
.f3 .input-field > label:not(.label-icon).active {
  -webkit-transform: translateY(-8px) scale(0.8);
  transform: translateY(-8px) scale(0.8);
}
</style>
