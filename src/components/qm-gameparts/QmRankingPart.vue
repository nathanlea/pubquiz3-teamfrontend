<template>
  <div class="ranking-part">
    <b-list-group flush>
        <b-list-group-item v-for="team in qmTeamsSorted" :key="team.id">
            <b-media>
            <template #aside>
                <h1 :title="$t('TOTAL_NUMBER_OF_POINTS')">
                {{ team.totalScore }}
                </h1>
                <!-- <b-img blank blank-color="#abc" width="64" alt="placeholder"></b-img> -->
            </template>
            <h5 class="mt-0 mb-1">{{ team.name }}</h5>
            <p class="mb-0">
                {{ team.memberNames }}
            </p>
            <p class="mb-0 d-none">
                TODO: score in this quiz section, trend (going up or sinking).
            </p></b-media
            >
        </b-list-group-item>
    </b-list-group>
    </div>
</template>

<script lang="ts">
import GameServiceMixin from '@/services/game-service-mixin';
import Vue from 'vue';
import Component, { mixins } from 'vue-class-component';
import { Game, Interaction, InteractionType, QuizItem, InteractionResponse, Team } from '../../models/models';
@Component
export default class QmRankingPart extends mixins(GameServiceMixin) {
  public name = 'QmRankingPart';

  get qmTeams(): Team[] {
    return this.$store.state.qmTeams;
  }

  get qmTeamsSorted(): Team[] {
    return this.$store.state.qmTeams.sort((a: Team, b: Team) => b.totalScore - a.totalScore);
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.grid-container {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: 1fr;
  grid-template-areas: "teamfeed quiz-container";
  overflow: hidden;
}

.grid-container > * {
  border-right: 4px solid #212529;
  /* padding: 0.5em; */
}

.ranking-part {
  grid-area: ranking-part;
  overflow: auto;
}
</style>
