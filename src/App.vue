<template>
  <main>
    <header>
      <h1>TODO</h1>
      <div class="mode">
        <img
          src="./assets/Frontend-mentor/images/icon-sun.svg"
          alt="sun icon"
          @click="toggleDarkMode"
          :class="{ darkIcon }"
        />
      </div>
    </header>

    <div class="container">
      <div
        class="input-container"
        :style="{
          'background-color': isDarkMode ? 'hsl(235, 24%, 19%)' : 'white',
        }"
      >
        <button class="checkbox" @click="addItem"></button>
        <form @submit="addItem">
          <input
            :style="{
              'background-color': isDarkMode ? 'hsl(235, 24%, 19%)' : 'white',
            }"
            class="todo-new"
            type="text"
            name="todo create"
            placeholder="Create a new todo..."
            v-model="newItem"
          />
        </form>
      </div>
      <div
        class="todos"
        :style="{
          'background-color': isDarkMode ? 'hsl(235, 24%, 19%)' : 'white',
        }"
      >
        <div
          class="item"
          v-for="item in items"
          v-bind:item="item"
          :class="{ completed: item.completed }"
          v-bind:key="item.id"
        >
          <div class="title-check">
            <button
              class="checkbox"
              @click="doneItem(item.id)"
              :class="{ active: isButtonClicked }"
              v-on:click="isButtonClicked = !isButtonClicked"
            ></button>
            <h2>{{ item.title }}</h2>
          </div>
          <button class="cross" @click="deleteItem">
            <img src="./assets/Frontend-mentor/images/icon-cross.svg" alt="" />
          </button>
        </div>
        <div
          class="todos-footer"
          :style="{
            'background-color': isDarkMode ? 'hsl(235, 24%, 19%)' : 'white',
          }"
        >
          <p>{{ items.filter((item) => !item.completed).length }} items left</p>

          <button class="clear" @click="clearCompletedItems">
            clear completed
          </button>
        </div>
      </div>

      <div
        class="bottom-sort"
        :style="{ 'background-color': isDarkMode ? '' : 'white' }"
      >
        <p @click="showAll">All</p>
        <p @click="showActive">Active</p>
        <p @click="showCompleted">Completed</p>
      </div>
    </div>

    <div class="attribution">
      Challenge by
      <a href="https://www.frontendmentor.io?ref=challenge" target="_blank">
        Frontend Mentor</a
      >. Coded by <a href="https://github.com/JustKooba">JustKooba</a>.
    </div>
  </main>
</template>

<script>
export default {
  data() {
    return {
      itemsLeft: null,
      newItem: "",
      items: [],
      originalItems: [],
      isDarkMode: true,
      isButtonClicked: false,
    };
  },
  methods: {
    addItem() {
      if (this.newItem.trim().length === 0) {
        return;
      }
      this.items.push({
        title: this.newItem,
        completed: false,
        id: Math.random(),
      });
      this.newItem = "";
    },
    doneItem(id) {
      const item = this.items.find((el) => el.id === id);
      item.completed = !item.completed;
      this.completedBtn = !this.completedBtn;
    },

    clearCompletedItems() {
      this.items = this.items.filter((item) => !item.completed);
      localStorage.deleteItem("item.completed", JSON.stringify(this.items));
    },
    showActive() {
      this.items = this.originalItems.filter((item) => !item.completed);
    },
    showCompleted() {
      this.items = this.originalItems.filter((item) => item.completed);
    },
    showAll() {
      this.items = [...this.originalItems];
    },

    toggleDarkMode() {
      document.body.classList.toggle("light");
      this.isDarkMode = !this.isDarkMode;
      this.darkIcon = !this.darkIcon;
      document.body.back.toggle("dark");
    },
    deleteItem(id) {
      const index = this.items.findIndex((el) => el.id === id);
      this.items.splice(index, 1);
    },
  },
  updated() {
    localStorage.setItem("items", JSON.stringify(this.items));
  },
  created() {
    this.items = JSON.parse(localStorage.getItem("items")) || [];
    this.originalItems = [...this.items];
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Josefin+Sans:wght@400;700&display=swap");

:root {
  --Bright-Blue: hsl(220, 98%, 61%);

  --Very-Light-Gray: hsl(0, 0%, 98%);
  --Very-Light-Grayish-Blue: hsl(236, 33%, 92%);
  --Light-Grayish-Blue: hsl(233, 11%, 84%);
  --Dark-Grayish-Blue: hsl(236, 9%, 61%);
  --Very-Dark-Grayish-Blue: hsl(235, 19%, 35%);

  --Very-Dark-Blue: hsl(235, 21%, 11%);
  --Very-Dark-Desaturated-Blue: hsl(235, 24%, 19%);
  --Light-Grayish-Blue: hsl(234, 39%, 85%);
  --Light-Grayish-Blue-hover: hsl(236, 33%, 92%);
  --Dark-Grayish-Blue: hsl(234, 11%, 52%);
  --Very-Dark-Grayish-Blue: hsl(233, 14%, 35%);
  --Very-Dark-Grayish-Blue: hsl(237, 14%, 26%);
}

*,
*::before,
*::after {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

body {
  background-color: var(--Very-Dark-Blue);
  color: var(--Light-Grayish-Blue);
  background-image: url("./assets/Frontend-mentor/images/bg-mobile-dark.jpg");
  background-repeat: no-repeat;
  background-position: top;
  background-size: 100%;
  padding: 30px;
  font-family: "Josefin Sans", sans-serif;
}

img {
  min-width: 100%;
}

header img {
  height: 25px;
  margin-top: 10px;
  cursor: pointer;
}

header {
  display: flex;
  justify-content: space-between;
  font-size: 25px;
  letter-spacing: 10px;
  color: #fff;
  font-weight: 300;
}

.todo-new,
.input-container,
.todos,
.bottom-sort,
.todos-footer {
  background-color: var(--Very-Dark-Desaturated-Blue);
}

.input-container {
  margin-bottom: 20px;
  border-radius: 7px;
  display: flex;
  padding: 7px;
  display: flex;
  align-content: center;
  margin-top: 30px;
}

a {
  color: rgb(0, 132, 255);
}

.attribution {
  margin-top: 20px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.todo-new {
  border-radius: 7px;
  font-family: inherit;
  border: none;
  height: 40px;
  font-size: 20px;
  width: 88%;
  outline: none;
}

.checkbox {
  background-color: transparent;
  border: 1px solid var(--Very-Dark-Grayish-Blue);
  width: 25px;
  height: 25px;
  border-radius: 50%;
  margin-top: 5px;
  margin-left: 10px;
  margin-right: 20px;
}

.todos {
  border-radius: 7px;
  padding: 10px;
  margin-bottom: 20px;
}

.completed {
  text-decoration: line-through;
  color: var(--Dark-Grayish-Blue);
}

.item {
  display: flex;
  align-items: center;
  flex-direction: row;
  justify-content: space-between;
  font-size: 10px;
  font-weight: 300;
  font-family: inherit;
  margin-bottom: 10px;
  padding-bottom: 7px;
  border-bottom: 1.5px solid var(--Very-Dark-Grayish-Blue);
}

button {
  cursor: pointer;
}

.cross {
  background-color: transparent;
  border: none;
  position: relative;
  margin-right: 20px;
}

.title-check {
  display: flex;
  justify-content: center;
  align-items: center;
}

.todos-footer {
  display: flex;
  justify-content: space-between;
  padding: 10px;
}

.todos-footer button {
  font-family: inherit;
  background-color: transparent;
  border: none;
  color: var(--Light-Grayish-Blue);
}

.bottom-sort {
  padding: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 7px;
}

.bottom-sort p {
  padding: 10px;
  color: var(--Dark-Grayish-Blue);
  font-weight: 700;
  cursor: pointer;
}

.light {
  background-color: var(--Very-Light-Grayish-Blue);
  color: black;
}

.darkIcon {
  background-image: url("./assets/Frontend-mentor/images/icon-moon.svg");
}

.active {
  background: linear-gradient(hsl(192, 100%, 67%) to hsl(280, 87%, 65%));
}

@media (min-width: 767px) {
  .container {
    width: 400px;
  }
  body {
    display: flex;
    justify-content: center;
    align-items: center;
  }
}
</style>
