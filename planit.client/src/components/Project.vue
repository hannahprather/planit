<template>
  <h5 class="selectable p-3" @click="goTo">{{ project.name }}</h5>
  <h5 class="p-3">{{ new Date(project.createdAt).toLocaleString() }}</h5>
  <h5>
    <i
      v-if="account.id == project.creatorId"
      class="mdi mdi-delete selectable"
      title="delete"
      @click="deleteProject(project.id)"
    ></i>
  </h5>
</template>


<script>
import { computed } from "@vue/reactivity"
import { AppState } from "../AppState"
import { router } from "../router"
import { projectService } from "../services/ProjectService"
import { logger } from "../utils/Logger"
import { Offcanvas } from "bootstrap"
export default {
  props: {
    project: {
      type: Object,
      required: true,
    },
  },
  setup(props) {
    return {
      account: computed(() => AppState.account),
      goTo() {
        router.push({ name: "Project", params: { id: props.project.id } })
        Offcanvas.getOrCreateInstance(document.getElementById('offcanvas')).hide()
      },
      deleteProject(id) {
        logger.log("deleting from deleter", id)
        projectService.deleteProject(id);

      }
    }
  }
}
</script>


<style lang="scss" scoped>
</style>