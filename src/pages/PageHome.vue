<template>
  <q-page>
    <div class="q-py-lg q-px-md row items-end q-col-gutter-md">
      <div class="col">
        <q-input
          bottom-slots
          class="new-qweet"
          v-model="newQweetContent"
          placeholder="What's Happening?"
          counter
          maxlength="250"
          autogrow
        >
          <template v-slot:before>
            <q-avatar>
              <img src="https://avatars.githubusercontent.com/u/59036987?v=4" />
            </q-avatar>
          </template>

          <template v-slot:append>
            <q-icon
              v-if="newQweetContent !== ''"
              name="close"
              @click="newQweetContent = ''"
              class="cursor-pointer"
            />
          </template>
        </q-input>
      </div>
      <div class="col col-shrink">
        <q-btn
          @click="setNewQweet"
          unelevated
          rounded
          color="primary"
          label="Qweet"
          no-caps
          :disabled="!newQweetContent"
          class="q-mb-lg"
        />
      </div>
    </div>

    <q-separator size="10px" color="grey-2" class="divider" />

    <q-list separator>
      <q-item
        clickable
        v-ripple
        class="q-py-md q-mb-md"
        v-for="qweet in qweets"
        :key="qweet.id"
      >
        <q-item-section avatar top>
          <q-avatar>
            <img src="https://cdn.quasar.dev/img/avatar2.jpg" />
          </q-avatar>
        </q-item-section>

        <q-item-section>
          <q-item-label class="text-subtitle1">
            <strong>{{ qweet.name }}</strong>
            <span class="text-grey-7">{{ qweet.username }}</span>
          </q-item-label>
          <q-item-label class="qweet-content text-body1">
            {{ qweet.content }}
          </q-item-label>

          <div class="row justify-between q-mt-sm qweet-icons">
            <q-btn flat round color="grey" size="sm" icon="far fa-comment" />
            <q-btn flat round color="grey" size="sm" icon="fas fa-retweet" />
            <q-btn flat round color="grey" size="sm" icon="far fa-heart" />
            <q-btn
              flat
              round
              color="grey"
              size="sm"
              icon="fa fa-trash"
              @click="deleteQweet(qweet.id)"
            />
          </div>
        </q-item-section>

        <q-item-section side top>
          {{ relativeDate(qweet.date) }}
        </q-item-section>
      </q-item>
    </q-list>
  </q-page>
</template>

<script>
import { formatDistance, subDays } from "date-fns";

export default {
  name: "PageHome",
  data() {
    return {
      newQweetContent: "",
      qweets: [
        {
          username: "@Lorainecyber1x32",
          name: "Loraine",
          content:
            "JavaScript é uma linguagem de programação bastante popular no desenvolvimento web.",
          date: 1683435854866,
          id: 0,
        },
        {
          username: "@egirlqcoda",
          name: "Larissa",
          content:
            "A programação orientada a objetos é um paradigma de programação que se baseia na utilização de objetos para representar dados e comportamentos.",
          date: 1683435866848,
          id: 1,
        },
        {
          username: "@OprimoDev",
          name: "André Alves",
          content:
            "CSS é uma linguagem de folhas de estilo utilizada para definir a aparência de documentos HTML.",
          date: 1683435873689,
          id: 2,
        },
        {
          username: "@DevInveste",
          name: "Lázaro",
          content:
            "O desenvolvimento ágil de software é uma abordagem para o desenvolvimento de software que se baseia em entregas frequentes e interação com o cliente.",
          date: 1651775870165,
          id: 3,
        },
      ],
    };
  },

  methods: {
    relativeDate(value) {
      return formatDistance(value, new Date());
    },

    deleteQweet(id) {
      this.qweets = this.qweets.filter((item) => item.id != id);
    },
    setNewQweet() {
      this.qweets.unshift({
        username: "@eulazzo",
        name: "Lázaro",
        content: this.newQweetContent,
        date: Date.now(),
        id: Math.floor(Math.random() * 10000),
      });
    },
  },
};
</script>

<style scoped lang="sass">
.new-qweet
  textarea
    font-size: 19px
    line-height: 1.4

.divider
  border-top: 1px solid
  border-bottom:1px solid
  border-color:$grey-4

.qweet-content
  white-space: pre-line

.qweet-icons
  margin-left: -5px
</style>
