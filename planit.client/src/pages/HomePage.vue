<template>
  <div class="container-fluid">
    <div v-if="!account.id">
      <h1 class="text-center text-primary">Please Log In to View Projects</h1>

      <!-- TODO Style me later bro, this is for not logged in -->
    </div>

    <div v-else>
      <b
        title="Create Post"
        class="
          create-btn
          btn btn-success
          text-white
          rounded-pill
          shadow
          d-flex
          align-items-center
          justify-content-center
        "
        data-bs-toggle="modal"
        data-bs-target="#project-modal"
      >
        <i class="mdi mdi-plus"></i>
      </b>

      <div class="row justify-content-center">
        <div class="col-6">
          <h2 class="text-center text-primary p-3 align-center">
            Your Projects
          </h2>
        </div>
      </div>
      <div class="row justify-content-center rounded">
        <div class="col-8 shadow bg-grey p-3">
          <div
            class="d-flex flex-row justify-content-between text-primary"
            v-for="p in projects"
            :key="p.id"
          >
            <Project :project="p" />
          </div>
        </div>
      </div>
    </div>
    <Modal id="project-modal">
      <template #modal-title>New Project</template>
      <template #modal-body><CreateProjectForm /></template>
    </Modal>
  </div>
</template>

<script>
import { computed } from "@vue/reactivity"
import { AppState } from "../AppState"
export default {
  name: 'Home',
  setup() {
    return {
      account: computed(() => AppState.account),
      projects: computed(() => AppState.projects)
    }
  }
}
</script>

<style scoped lang="scss">
.home {
  display: grid;
  height: 80vh;
  place-content: center;
  text-align: center;
  user-select: none;
  .home-card {
    width: 50vw;
    > img {
      height: 200px;
      max-width: 200px;
      width: 100%;
      object-fit: contain;
      object-position: center;
    }
  }
}
.create-btn {
  font-size: 20px;
  height: 60px;
  width: 60px;
  z-index: 100;
  position: fixed;
  top: 12vh;
  left: 5vh;
}
</style>
