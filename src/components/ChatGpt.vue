<template>
  <div>
    <h1>Chat</h1>
    <div class="message-container chat_fondo">
      <div v-for="(message, index) in messages" :key="index">
        <p v-if="index%2 ==0" class="chat_of_cliente">{{ message.text }}</p>
        <p v-else class="chat_of_chatgpt">{{ message.text }}</p>
        <small>sent by {{ message.user }} at {{ message.timestamp }}</small>
      </div>
    </div>
    <!-- <h1>Chat 2</h1>
    <div class="message-container">
      <div v-for="(message, index) in messages" :key="index">
        <p class="text-danger">{{ message.text }}</p>
        <small>sent by {{ message.user }} at {{ message.timestamp }}</small>
      </div>
    </div> -->
    <input
      type="text"
      v-model="newMessage"
      @keyup.enter="sendMessage"
      placeholder="Type your message..."
    />
  </div>
</template>

<script>
import { defineComponent } from 'vue'
import axios from 'axios'

export default defineComponent({
  name: 'chat_gpt',
  data() {
    return {
      messages: [
        // { text: 'Hello!', user: 'User 1', timestamp: '2022-03-27 10:30:00' },
        // { text: 'Hi there!', user: 'User 2', timestamp: '2022-03-27 10:31:00' },
        // { text: 'How are you?', user: 'User 1', timestamp: '2022-03-27 10:32:00' }
      ],
      newMessage: ''
    }
  },
  methods: {
    sendMessage() {
      const timestamp = new Date().toISOString()
      console.log('entra y funciona jjj', this.newMessage)
      this.messages.push({ text: this.newMessage, user: this.currentUser, timestamp })
      axios
        .post('http://127.0.0.1:8000/api/chatbot', {text: this.newMessage})
        .then((response) => {
          console.log(response.data)
          this.messages.push({ text: response.data, user: this.currentUser, timestamp })
        })
        .catch((error) => {
          console.log(error)
          console.log(error.message)

        })
      this.newMessage = ''

    }
  }
})
</script>

<style scoped>
h1{
  color: rgb(197, 28, 28);
}

.chat_of_chatgpt{
  color: rgb(2, 2, 2);
  background-color: rgb(239, 145, 190);
}

.chat_of_cliente{
  color: rgb(7, 7, 7);
  background-color: rgb(91, 69, 232);
}
.chat_fondo{
  background-color: rgb(17, 62, 121);
}
</style>