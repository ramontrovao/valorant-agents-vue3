<script lang="ts" setup>
import { RouterLink } from 'vue-router';

    export interface IAgentCardProps {
        agentUuid: string;
        agentName: string;
        agentImageSrc: string;
        agentRole: string;
    }

    withDefaults(defineProps<IAgentCardProps>(), {
        agentRole: "Sem classe"
    })
</script>

<template>
  <RouterLink
    :to="`/agent/${agentUuid}`"
    class="agent-card"
  >
    <div class="agent-infos">
      <strong>{{ agentName }}</strong>

      <div class="agent-roles">
        <div>
          <p>{{ agentRole }}</p>
        </div>
      </div>
    </div>

    <img
      :src="agentImageSrc"
      class="agent-img"
      alt=""
    >
  </RouterLink>
</template>

<style lang="scss" scoped>
    @import "../assets/vars.scss";

    .agent-card {
        min-width: 19.5rem;
        height: 10rem;
        padding: 2rem 0 2rem 2rem;

        display: flex;
        justify-content: space-between;
        align-items: center;

        text-decoration: none;
        overflow: hidden;
        background: linear-gradient(to right, #d3cce3, #eFF4f0);
        border-radius: 16px;
        transition: 0.4s;

        strong {
            font-size: $text-md;
        }

        &:hover {
        scale: 1.05;
        }

        @media (max-width: 425px) {
            min-width: 17rem;
        }
    }

    .agent-infos {
        max-height: 7rem;

        display: flex;
        flex-direction: column;
        align-items: flex-start;
        justify-content: center;
        gap: 1rem;

        strong, p {
            color: #000;
        }
    }

    .agent-img {
        max-width: 10rem;
        max-height: 10rem;
    }
</style>