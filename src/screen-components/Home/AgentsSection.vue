<script lang="ts" setup>
    import { onMounted, ref, watch, type Ref } from "vue";

    import { getValorantAgents } from "../../services/api"
    import type { TAgent } from "@/types/Agent";

    import { searchQ } from "../../shared/searchQ"

    import AgentCard from "../../components/AgentCard.vue"
    import Loading from "../../components/Loading.vue"

    const agents: Ref<{ status: number, data: TAgent[] } | null> = ref(null)

    const fetchAgents = async () => {
        try {
            const agentsData = await getValorantAgents()

            agents.value = agentsData.data
        } catch (err) {
            console.log(err)
        }
    }

    watch(() => searchQ.text, () => {
        console.log(searchQ.text)
    })

    onMounted(fetchAgents)
</script>

<template>
  <section
    v-if="agents?.data"
    class="valorant-agents-section"
  >
    <AgentCard
      v-for="agent in agents.data"
      :key="agent.uuid"
      :agent-uuid="agent.uuid"
      :agent-name="agent.displayName"
      :agent-role="agent.role?.displayName"
      :agent-image-src="agent.displayIcon"
    />
  </section>

  <section
    v-else
    class="loading-section"
  >
    <Loading />
  </section>
</template>

<style lang="scss" scoped>
    .valorant-agents-section {
        margin: auto;
        width: 100%;
        max-width: 1300px;
        padding: 8.125rem 1.5rem 1.5rem 1.5rem;

        display: grid;
        place-items: center;
        grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
        gap: 3.125rem;

        @media (max-width: 768px) {
          padding: 10.125rem 1rem 1rem 1rem;
        }
    }

    .loading-section {
        height: 100vh;

        display: flex;
        justify-content: center;
        align-items: center;
    }
</style>