<template>
  <section class="sessions">
    <SubHeader :subheader="headline" />
    <form class="sessions__inputform">
      <div class="sessions__input-wrapper">
        <label for="titleSession">Title</label>
        <input
          type="text"
          id="titleSession"
          v-model="title"
          placeholder="Title of your new session"
        />
        <label for="descriptionSession">Description</label>
        <input
          type="text"
          id="descriptionSession"
          v-model="description"
          placeholder="Description of your new session"
        />
        <div class="buttons">
          <button
            @click.prevent="AddSessionData(this.title, this.description)"
            class="sessions__add-button"
          >
            Add Session
          </button>
          <button
            @click.prevent="
              $router.push({
                name: 'manage',
              })
            "
            class="sessions__cancel-button"
          >
            Cancel
          </button>
        </div>
      </div>
    </form>
  </section>
</template>

<script>
export default {
  data() {
    return {
      title: "",
      description: "",
      newSession: {},
      headline: "Create your Session",
    };
  },
  methods: {
    async AddSessionData(title, description) {
      this.newSession = { title, description };
      const response = await fetch(
        process.env.VUE_APP_API_BASE_URL + "/sessions",
        {
          method: "POST",
          headers: { "Content-type": "application/json" },
          body: JSON.stringify(this.newSession),
        }
      );
      this.newSession = await response.json();

      this.$router.push({
        name: "edit",
        params: { id: this.newSession.id },
      });
    },
  },
};
</script>

<style scoped>
.sessions {
  margin: 0 auto;
  width: 100%;
  margin-bottom: 2rem;
}
.sessions__inputform {
  display: flex;
  flex-direction: column;
}
.buttons {
  grid-area: button;
  display: inline-flex;
  justify-content: space-evenly;
}
.sessions__add-button,
.sessions__cancel-button {
  all: unset;
  font-size: 20px;
  font-weight: 600;
  color: var(--clr-primary);
  background-color: var(--clr-surface);
  border: 2px solid var(--clr-primary);
  box-shadow: 3.5px 3.5px 0px var(--clr-dark-purple);
  padding: 0.5rem 1.25rem;
  border-radius: 2px;
  margin-top: 1rem;
  cursor: pointer;
}

.sessions__add-button:hover,
.sessions__cancel-button:hover {
  background: var(--clr-primary);
  border: 2px solid var(--clr-primary);
  color: var(--clr-surface);
}

.sessions__add-button:active,
.sessions__cancel-button:active {
  box-shadow: none;
}

.sessions__input-wrapper {
  display: grid;
  grid-template-columns: fit-content(100px) 1fr;
  column-gap: 1rem;
  row-gap: 1rem;
  grid-template-areas:
    "title title-text"
    "description description-text"
    "button button";
  align-items: center;
  padding: 3rem;
  box-shadow: var(--clr-primary) 0px 2px 5px 0px,
    var(--clr-primary-inactive) 0px 1px 1px 0px;
}

input {
  padding: 1rem;
  background: var(--clr-surface);
  border: 2px solid var(--clr-primary-inactive);
}

input:focus-within {
  outline: none;
  border: 2px solid var(--clr-primary);
}

::placeholder {
  color: var(--clr-primary-inactive);
}

label {
  font-weight: 600;
}
</style>
