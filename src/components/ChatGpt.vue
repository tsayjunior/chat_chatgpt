<template>
  <div>
    <h1>Chat</h1>
    <div class="message-container">
      <div v-for="(message, index) in messages" :key="index">
        <p>{{ message.text }}</p>
        <small>sent by {{ message.user }} at {{ message.timestamp }}</small>
      </div>
    </div>
    <input type="text" v-model="newMessage" @keyup.enter="sendMessage" placeholder="Type your message...">
  </div>
</template>

<script>
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'chat_gpt',
  data() {
    return {
      messages: [
        { text: 'Hello!', user: 'User 1', timestamp: '2022-03-27 10:30:00' },
        { text: 'Hi there!', user: 'User 2', timestamp: '2022-03-27 10:31:00' },
        { text: 'How are you?', user: 'User 1', timestamp: '2022-03-27 10:32:00' },
      ],
      newMessage: '',
    };
  },
  methods: {
    sendMessage() {
      const timestamp = new Date().toISOString();
      this.messages.push({ text: this.newMessage, user: this.currentUser, timestamp });
      this.newMessage = '';
    },
  },
});
</script>
