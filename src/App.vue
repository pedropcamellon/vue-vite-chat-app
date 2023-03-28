<script setup>
import { ref } from 'vue'

const users = ref([
  {
    id: 0,
    name: "Peter"
  },
  {
    id: 1,
    name: "Paul"
  },
])

const messages = ref(
  [
    {
      id: 0,
      senderId: 0,
      body: "Hi!",
      created_at: "10:19 AM"
    },
    {
      id: 1,
      senderId: 1,
      body: "Hello!",
      created_at: "10:21 AM"
    },
    {
      id: 2,
      senderId: 0,
      body: "Hello!",
      created_at: "10:22 AM"
    }
  ]
)

let newMessageBody = ref('')

let id = 4;

function onSendMessage() {
  messages.value = [
    ...messages.value,
    {
      id: id++,
      senderId: 0,
      body: newMessageBody.value,
      created_at: new Date().toLocaleTimeString("en-us", { hour: "2-digit", minute: "2-digit" })
    }
  ]
}

</script>

<template>
  <div class="app">
    <h2>Chat</h2>
    <!-- CHAT ROOM -->
    <!-- Messages -->
    <ul class="chat-room">
      <li v-for="message in messages" :key="message.id" class="flex column">
        <p class="message" :class="message.senderId === 0 ? 'sender' : 'not-sender'">
        <p class="message-body" :class="message.senderId === 0 ? 'sender-body' : 'not-sender-body'">
          {{ message.body }}
        </p>
        <span>{{ message.created_at + ' ' + users[message.senderId].name }}</span>
        </p>
      </li>
    </ul>

    <!-- New Message -->
    <form @submit.prevent="onSendMessage" class="new-msg-form">
      <input v-model="newMessageBody" placeholder="" class="new-msg-form__body" />
      <input type="submit" value="Send" class="new-msg-form__send-btn" />
    </form>

  </div>
</template>

<style scoped>
.flex {
  display: flex;
}

.column {
  flex-direction: column;
}

.app {
  height: 90vh;
}

.chat-room {
  height: 70vh;
  padding: 1rem;
  margin: 0;
  overflow-y: scroll;
  background-color: rgb(212, 212, 212);
}

.message {
  max-width: fit-content;
}

.message-body {
  padding: 1rem 1.5rem;
  border-radius: 1rem;
}

.sender {
  margin-left: auto;
}

.sender-body {
  background-color: beige;
}

.not-sender {
  /*  */
}

.not-sender-body {
  background-color: cadetblue;
}

.new-msg-form {
  display: flex;
  padding: 0.5rem 1rem;
  background-color: rgb(115, 119, 119);
}

.new-msg-form__body {
  flex-grow: 1;
  margin-right: 0.5rem;
  border-radius: 1rem;
}

.new-msg-form__send-btn {
  padding: 1rem;
  border-radius: 1rem;
}
</style>