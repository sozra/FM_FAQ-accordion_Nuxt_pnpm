<template>
  <div>
    <!-- <NuxtWelcome /> -->

    <article v-for="(item, index) in faqList" :key="index">
      <header class="accordion-header expanded">
        <h2>{{ item.question }}</h2>
        <button></button>
      </header>
      <p>{{ item.answer }}</p>
    </article>

  </div>
</template>

<script setup>
function test(index) {
  console.log('trigger test function', index);
  let tag = document.getElementById("testt");
  const classList = tag.classList;
  if (classList.contains("test")) {
    classList.remove("test");
  } else {
    classList.add("test");
  }
};

const faqList = reactive([
  {
    question: "What is Frontend Mentor, and how will it help me?",
    answer: "Frontend Mentor offers realistic coding challenges to help developers improve their\
      frontend coding skills with projects in HTML, CSS, and JavaScript. It's suitable for\
      all levels and ideal for portfolio building."
  },
  {
    question: "Is Frontend Mentor free?",
    answer: "Yes, Frontend Mentor offers both free and premium coding challenges, with the free\
    option providing access to a range of projects suitable for all skill levels."
  },
  {
    question: "Can I use Frontend Mentor projects in my portfolio?",
    answer: "Yes, you can use projects completed on Frontend Mentor in your portfolio. It's an excellent\
    way to showcase your skills to potential employers!"
  },
  {
    question: "How can I get help if I'm stuck on a Frontend Mentor challenge?",
    answer: "The best place to get help is inside Frontend Mentor's Discord community. There's a help\
    channel where you can ask questions and seek support from other community members."
  }
])

</script>


<style lang="scss" scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  border: 1px solid black;
  padding: 1rem;


  // h2 {
  //   color: red;
  // }
}

.attribution {
  a {
    background-color: red;
  }
}

.accordion-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  border: 1px solid black;
  padding: 1rem;

  button {
    // background-color: lightblue;
    background-color: transparent;
    border-radius: 30%;
    border: none;
    font-size: 2.5rem;
    transition: all 0.3s ease-in-out;

    &::before {
      content: "+";
    }

    // &:not(.expanded)::before {
    //   content: "+";
    // }
    // &.expanded::before {
    //   content: "-";
    // }
    &:focus,
    &:active {
      outline: rgb(from color r g b);
    }

    &:hover {
      // background-color: lightblue;
      scale: 1.2;
      transform-origin: center;
    }
  }

  // button+p {
  //     max-width: 0;
  //     overflow: hidden;
  //     transition: all 0.3s ease-in-out;
  //     }
  //   button.expanded+p {
  //     max-width: 100%;
  //   }



  &.expanded {
    button {
      // background-color: lightblue;
      scale: 1.2;
      transform-origin: center;

      &::before {
        content: "-";
      }
    }

    &+p {
      max-height: 100%;
    }
  }
}


p {
  max-height: 0;
  overflow: hidden;
  transition: all 0.3s ease-in-out;
}

//   .anwser  {
//     overflow: hidden;
//   }
</style>