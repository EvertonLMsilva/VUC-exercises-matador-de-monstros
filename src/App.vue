<template>
  <div class="AppContainer">
    <!-- componente jogador -->
    <div class="AppJogadores AppPaper">
      <Jogador namePlayer="Jogador" :life="state.player" width="40%" />
      <Jogador namePlayer="Monstro" :life="state.monster" width="40%" />
    </div>

    <div class="AppPaper AppResult" style="color: red" v-if="state.player <= 0">
      Você perdeu (┬┬﹏┬┬)
    </div>
    <div
      class="AppPaper AppResult"
      style="color: green"
      v-else-if="state.monster <= 0"
    >
      Você ganhou (●'◡'●)
    </div>

    <!-- Componente botão -->
    <div class="AppPaper" v-show="!state.showOptions">
      <RfButton
        nameButton="Inciar novo Jogo"
        @click="state.showOptions = true"
      />
    </div>

    <div class="AppPaper" v-show="state.showOptions">
      <RfButton
        nameButton="ATAQUE"
        color="warnig"
        style="margin: 10px"
        @click="defaultAttack"
      />
      <RfButton
        nameButton="ATAQUE ESPECIAL"
        color="alert"
        style="margin: 10px"
        @click="specialAttack"
      />
      <RfButton
        nameButton="Curar"
        color="secondary"
        style="margin: 10px"
        @click="healPlayer"
      />
      <RfButton
        nameButton="DESISTIR"
        color="neutral"
        style="margin: 10px"
        @click="toGiveUp"
      />
    </div>

    <!-- Componete resultado do ataque -->
    <div v-show="state.monster < 100 || state.player < 100" class="AppPaper">
      <div v-for="(value, index) in state.logAttack" :key="index">
        <div
          class="logAttack"
          :style="{
            backgroundColor:
              name === 'player' || name === 'heal' ? '#0175d4' : '#9b6a00',
          }"
          v-for="(itens, name, indexObj) in value"
          :key="indexObj"
        >
          <span v-if="name == 'heal'">
            Jogador ganhou força de {{ itens }}
          </span>
          <span v-else>
            {{ name === "player" ? "Jogador" : "Monstro" }} atacou o
            {{ name === "player" ? "monstro" : "jogador" }} com {{ itens }}
          </span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Jogador from "./components/jogador.vue";
import RfButton from "./components/v1/Button/Button.vue";

export default {
  name: "App",

  data() {
    return {
      state: {
        showOptions: false,

        monster: 100,
        player: 100,

        logAttack: [],
        heal: 0,

        defaultAttackMonster: 15,
        defaultAttackPlayer: 10,
        specialAttackPlayer: 20,
      },
    };
  },

  components: {
    Jogador,
    RfButton,
  },

  methods: {
    attackDamage(attackMin, attackMax, entitie) {
      let keyObject = entitie === "player" ? "monster" : "player";

      const attack = Math.floor(
        Math.random() * (attackMax - attackMin) + attackMin
      );
      if (this.state.player <= 0 || this.state.monster <= 0) {
        return;
      }
      this.state[keyObject] -= attack;
      this.state.logAttack.push({ [entitie]: attack });
    },

    healPlayer() {
      const heal = Math.floor(
        Math.random() * (this.state.defaultAttackPlayer - 5) + 5
      );

      this.state.player += heal;

      if (this.state.player >= 100) {
        this.state.player = 100;
        return;
      }

      this.attackDamage(0, this.state.defaultAttackMonster, "monster");
      this.state.logAttack.push({ heal });
    },

    defaultAttack() {
      this.attackDamage(5, this.state.defaultAttackMonster, "monster");
      this.attackDamage(0, this.state.defaultAttackPlayer, "player");
    },

    specialAttack() {
      this.attackDamage(5, this.state.defaultAttackMonster, "monster");
      this.attackDamage(5, this.state.specialAttackPlayer, "player");
    },

    toGiveUp() {
      this.state.showOptions = false;
      this.state.logAttack = [];

      this.state.player = 100;
      this.state.monster = 100;
    },
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.AppContainer {
  display: flex;
  justify-content: space-around;
  flex-direction: column;

  .AppResult {
    font-size: 1.5em;
    font-family: Verdana, Geneva, Tahoma, sans-serif;
    font-weight: 700;
  }

  .AppPaper {
    margin-top: 50px;
    padding: 20px;
    border-radius: 15px;
    box-shadow: 4px 4px 8px #cccccc;
  }

  .AppJogadores {
    display: flex;
    justify-content: space-around;
    flex-direction: row;
    margin: 10px;
  }

  .logAttack {
    display: flex;
    justify-content: center;
    align-items: center;
    margin: 10px;
    height: 45px;
    font-size: 1.5em;
    color: #fff;
  }
}
</style>
