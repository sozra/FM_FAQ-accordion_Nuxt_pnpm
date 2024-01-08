<template>
  <div class="faq-background">
    <section class="faq-card">
      <h1>FAQs</h1>
      <!-- <NuxtWelcome /> -->
      <article v-for="(item, index) in faqList" :key="index" :id="'article' + index">
        <!-- <article v-for="(item, index) in faqList" :key="index" :id="'article'+index" :style="{'--max': setMaxHeight(index)}"> -->
        <button class="accordion-header" :class="{ 'expanded': currentExpandedIndex === index }" :id="'header' + index"
          @click="test(index)">
          <!-- <header class="accordion-header expanded" :id="'header' + index"> -->
          <h2>{{ item.question }}</h2>
          <img :src="`/_nuxt/public/assets/images/icon-${currentExpandedIndex == index ? 'minus' : 'plus'}.svg`" alt="">
          <!-- </header> -->
        </button>
        <p :id="'answer' + index">{{ item.answer }}</p>
      </article>

    </section>
  </div>
</template>

<script setup>
const currentExpandedIndex = ref(0);
function test(index) {
  console.log('trigger test function', index);
  // let tag = document.getElementById(`header${index}`);
  // const classList = tag.classList;
  // if (classList.contains("test")) {
  //   classList.remove("test");
  // } else {
  //   classList.add("test");
  // }
  const child = document.querySelector(`#answer${index}`);
  if (!child) return;
  console.log("child.scrollHeight", child.scrollHeight);
  console.log(`index: ${index}, currentExpandedIndex: ${currentExpandedIndex.value}`)
  if (index === currentExpandedIndex.value) {
    // child.style.maxHeight = child.scrollHeight + 'px';
    child.style.maxHeight = '0px';
    currentExpandedIndex.value = -1;
  }
  else {
    child.style.maxHeight = child.scrollHeight + 'px';
    if (currentExpandedIndex.value !== -1) {
      const prevChild = document.querySelector(`#answer${currentExpandedIndex.value}`);
      prevChild.style.maxHeight = '0px';
    }
    currentExpandedIndex.value = index;
  }
  console.log(`at LAST, index: ${index}, currentExpandedIndex: ${currentExpandedIndex.value}`)
};

onBeforeMount(()=>{
  console.log('onBeforeMount');
  const child = document.querySelector(`#answer0`);
  if (!child) return;
  child.style.maxHeight = child.scrollHeight + 'px';
  console.log('init changed')
})




function setMaxHeight(index) {
  return Math.floor(Math.random() * 100) + 'px';
};
function setMaxHeight1(index) {
  nextTick().then(() => {

    // const parent = document.querySelector(`article${index}`);
    const child = document.querySelector(`#answer${index}`);
    // debugger;
    console.log('child: ', child);

    if (!child) return;
    console.log("child.scrollHeight", child.scrollHeight);
    if (index === currentExpandedIndex.value) {
      return child.scrollHeight + 'px';
    }
    else {
      return '0px';
    }
  })
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
    // question: "How can I get help if I'm stuck on a Frontend Mentor challenge?",
    question: "How can I get help if I'm stuck on a challenge?",
    answer: "The best place to get help is inside Frontend Mentor's Discord community. There's a help\
    channel where you can ask questions and seek support from other community members."
  }
])

</script>


<style lang="scss" scoped>
$White: hsl(0, 0%, 100%);
$Light-pink: hsl(275, 100%, 97%);
$Grayish-purple: hsl(292, 16%, 49%);
$Dark-purple: hsl(292, 42%, 14%);
$font: WorkSans;

:root {
  box-sizing: border-box;
  padding: 0;
  margin: 0;
  font-family: $font;
}

h1,h2,p,button {
  font-family: $font;
}


div.faq-background {
  background-image: url('./public/assets/images/background-pattern-desktop.svg');
  background-size: 100%;
  background-repeat: no-repeat;
  background-color: $Light-pink;
  width: 100vw;
  height: 100vh;

}

section.faq-card {
  width: 600px;
  height: 566px;
  position: absolute;
  margin: auto auto;
  padding: 20px;
  background-color: white;
  inset: 0;
  border-radius: 20px;

  article {
    button {

      width: 100%;
      background-color: white;
      border: none;
      display: flex;
      justify-content: space-between;


      h2 {
        text-align: start;
        &:hover,
        &+img:hover,
        &:has(+img:hover) {
          color: $Grayish-purple;
          cursor: pointer;
        }
      }

    }

    p {
      max-height: 0px;
      overflow: hidden;
      transition: max-height .2s ease-in-out;
      // .expand {
      //   max-height: var(--max);
      // }
    }


    // &:nth-child(n+3) p {
    //   max-height: 0px;
    //   overflow: hidden;
    //   transition: max-height .2s ease-in-out;
    // }

  }
}
</style>