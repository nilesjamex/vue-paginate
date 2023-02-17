<template>
  <div class="home">
    <div v-for="item in currentPosts" :key="item.id">
      {{ item.desc }}
    </div>
    <div class="interview__pagination">
      <h6 @click="previous">Previous</h6>
      <div class="numbers">
        <p v-for="item in pageNumbers" :key="item" @click="currentPage = item">
          {{ item }}
        </p>
      </div>
      <h6 @click="next">Next</h6>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { watch } from "vue";
import { ref } from "@vue/reactivity";
interface Person {
  img: any;
  desc: string;
  date: string;
  field: string;
  id: number;
  bg: string;
}
const questions = ref<Person[]>([
  {
    img: `https://res.cloudinary.com/dx9pt4ggx/image/upload/v1675954449/zerotech/vue_sh8jo3.png`,
    desc: "Jessica Gabriel recently posted interview questions for UI/UX Designer",
    date: "Friday 5th, 2022 6:45pm",
    field: "UI/UX Designers",
    id: 1,
    bg: "#FFFFFF",
  },
  {
    img: `https://res.cloudinary.com/dx9pt4ggx/image/upload/v1675954449/zerotech/vue_sh8jo3.png`,
    desc: "Jessica Gabriel recently posted interview questions for UI/UX Designer",
    date: "Friday 5th, 2022 6:45pm",
    field: "UI/UX Designers",
    id: 2,
    bg: "#F9F2EE",
  },
  {
    img: `https://res.cloudinary.com/dx9pt4ggx/image/upload/v1675954449/zerotech/vue_sh8jo3.png`,
    desc: "Jessica Gabriel recently posted interview questions for UI/UX Designer",
    date: "Friday 5th, 2022 6:45pm",
    field: "UI/UX Designers",
    id: 3,
    bg: "#FFFFFF",
  },
  {
    img: `https://res.cloudinary.com/dx9pt4ggx/image/upload/v1675954449/zerotech/vue_sh8jo3.png`,
    desc: "Jessica Gabriel recently posted interview questions for UI/UX Designer",
    date: "Friday 5th, 2022 6:45pm",
    field: "UI/UX Designers",
    id: 4,
    bg: "#F9F2EE",
  },
  {
    img: `https://res.cloudinary.com/dx9pt4ggx/image/upload/v1675954449/zerotech/vue_sh8jo3.png`,
    desc: "Jessica Gabriel recently posted interview questions for UI/UX Designer",
    date: "Friday 5th, 2022 6:45pm",
    field: "UI/UX Designers",
    id: 5,
    bg: "#FFFFFF",
  },
  {
    img: `https://res.cloudinary.com/dx9pt4ggx/image/upload/v1675954449/zerotech/vue_sh8jo3.png`,
    desc: "Jessica Gabriel recently posted interview questions for UI/UX Designer",
    date: "Friday 5th, 2022 6:45pm",
    field: "UI/UX Designers",
    id: 6,
    bg: "#F9F2EE",
  },
  {
    img: `https://res.cloudinary.com/dx9pt4ggx/image/upload/v1675954449/zerotech/vue_sh8jo3.png`,
    desc: "Jessica Gabriel recently posted interview questions for UI/UX Designer",
    date: "Friday 5th, 2022 6:45pm",
    field: "UI/UX Designers",
    id: 7,
    bg: "#FFFFFF",
  },
  {
    img: `https://res.cloudinary.com/dx9pt4ggx/image/upload/v1675954449/zerotech/vue_sh8jo3.png`,
    desc: "Jessica Gabriel recently posted interview questions for UI/UX Designer",
    date: "Friday 5th, 2022 6:45pm",
    field: "UI/UX Designers",
    id: 8,
    bg: "#FFFFFF",
  },
  {
    img: `https://res.cloudinary.com/dx9pt4ggx/image/upload/v1675954449/zerotech/vue_sh8jo3.png`,
    desc: "Jessica Gabriel recently posted interview questions for UI/UX Designer",
    date: "Friday 5th, 2022 6:45pm",
    field: "UI/UX Designers",
    id: 9,
    bg: "#F9F2EE",
  },
  {
    img: `https://res.cloudinary.com/dx9pt4ggx/image/upload/v1675954449/zerotech/vue_sh8jo3.png`,
    desc: "Jessica Gabriel recently posted interview questions for UI/UX Designer",
    date: "Friday 5th, 2022 6:45pm",
    field: "UI/UX Designers",
    id: 10,
    bg: "#FFFFFF",
  },
  {
    img: `https://res.cloudinary.com/dx9pt4ggx/image/upload/v1675954449/zerotech/vue_sh8jo3.png`,
    desc: "Jessica Gabriel recently posted interview questions for UI/UX Designer",
    date: "Friday 5th, 2022 6:45pm",
    field: "UI/UX Designers",
    id: 11,
    bg: "#F9F2EE",
  },
  {
    img: `https://res.cloudinary.com/dx9pt4ggx/image/upload/v1675954449/zerotech/vue_sh8jo3.png`,
    desc: "Jessica Gabriel recently posted interview questions for UI/UX Designer",
    date: "Friday 5th, 2022 6:45pm",
    field: "UI/UX Designers",
    id: 12,
    bg: "#FFFFFF",
  },
  {
    img: `https://res.cloudinary.com/dx9pt4ggx/image/upload/v1675954449/zerotech/vue_sh8jo3.png`,
    desc: "Jessica Gabriel recently posted interview questions for UI/UX Designer",
    date: "Friday 5th, 2022 6:45pm",
    field: "UI/UX Designers",
    id: 13,
    bg: "#F9F2EE",
  },
  {
    img: `https://res.cloudinary.com/dx9pt4ggx/image/upload/v1675954449/zerotech/vue_sh8jo3.png`,
    desc: "Jessica Gabriel recently posted interview questions for UI/UX Designer",
    date: "Friday 5th, 2022 6:45pm",
    field: "UI/UX Designers",
    id: 14,
    bg: "#FFFFFF",
  },
]);

const totalPosts = questions.value.length;
const pageNumbers = ref<any>([]);
const postPerPage = ref<number>(5);
const currentPage = ref<number>(1);
const indexOfLastPost = ref<number>();
const indexOfFirstPost = ref<number>();
const currentPosts = ref<any>();

indexOfLastPost.value = currentPage.value * postPerPage.value;
indexOfFirstPost.value = indexOfLastPost.value - postPerPage.value;
currentPosts.value = questions.value.slice(
  indexOfFirstPost.value,
  indexOfLastPost.value
);
const paginateNumber = Math.ceil(totalPosts / postPerPage.value);
console.log(paginateNumber);

for (let i = 1; i <= Math.ceil(totalPosts / postPerPage.value); i++) {
  pageNumbers.value.push(i);
}
const previous = () => {
  if (currentPage.value > 1) {
    currentPage.value = currentPage.value - 1;
  }
};
const next = () => {
  if (currentPage.value >= 1 && currentPage.value < paginateNumber) {
    currentPage.value = currentPage.value + 1;
  }
};
watch(currentPage, (currentValue, oldValue) => {
  indexOfLastPost.value = currentValue * postPerPage.value;
  indexOfFirstPost.value = indexOfLastPost.value - postPerPage.value;
  console.log(indexOfLastPost.value);
  currentPosts.value = questions.value.slice(
    indexOfFirstPost.value,
    indexOfLastPost.value
  );
});
</script>
