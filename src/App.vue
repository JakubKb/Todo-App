<template>
  <main>
    <header>
      <h1>TODO</h1>
      <div class="mode">
        <img
          src="./assets/Frontend-mentor/images/icon-sun.svg"
          alt="sun icon"
        />
      </div>
    </header>

    <div class="container">
      <div class="input-container">
        <button class="checkbox" disabled="true"></button>
        <input
          class="todo-new"
          type="text"
          name="todo create"
          placeholder="Create a new todo..."
        />
      </div>
      <div class="todos">
        <div
          class="item"
          v-for="item in items"
          v-bind:item="item"
          v-bind:key="item.id"
        >
          <div class="title-check">
            <button class="checkbox"></button>
            <h2>{{ item.title }}</h2>
          </div>
          <button class="cross">
            <img src="./assets/Frontend-mentor/images/icon-cross.svg" alt="" />
          </button>
        </div>
      </div>
      <!--Dynamic Num-->

      <div class="todos-footer">items left clear completed</div>
      <div class="bottom-sort">Completed All Active</div>
    </div>

    <div class="attribution">
      Challenge by
      <a href="https://www.frontendmentor.io?ref=challenge" target="_blank"
        >Frontend Mentor</a
      >. Coded by <a href="#">Your Name Here</a>.
    </div>
  </main>
</template>

<script>
export default {
  data() {
    return {
      newItem: "",
      items: [
        { title: "Todo", completed: false, id: 1 },
        { title: "New todo", completed: false, id: 2 },
      ],
    };
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
  justify-content: center;
  align-content: center;
  margin-top: 30px;
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
  background-color: transparent !important;
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
</style>
