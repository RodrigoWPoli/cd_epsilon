<template>
    <div style="text-align: center; margin-top: 50px;">
      <div>
        <input
          type="text"
          placeholder="Write a message..."
          v-model="message"
          style="padding: 10px; justify-content: center;"
        />
        <button
          @click="handleSendMessage"
          style="padding: 10px; background-color: #4CAF50; color: white; border: none; cursor: pointer;"
        >
          Send
        </button>
      </div>
      <div style="margin: 20px auto;">Encrypted message:</div>
      <div
        style="
          margin: 20px auto;
          border: 2px solid #ddd;
          padding: 10px;
          height: 200px;
          max-width: 400px;
          word-wrap: break-word;
        "
      >
        <p v-if="encryptedMessage">{{ encryptedMessage }}</p>
      </div>
      <div style="margin: 20px auto;">Message received:</div>
      <div
        style="
          margin: 20px auto;
          border: 2px solid #ddd;
          padding: 10px;
          height: 200px;
          max-width: 400px;
          word-wrap: break-word;
        "
      >
        <p v-if="displayedMessage">{{ displayedMessage }}</p>
      </div>
    </div>
  </template>
  
  <script>
  import CryptoJS from 'crypto-js';
  
  export default {
    data() {
      return {
        message: '',
        displayedMessage: '',
        encryptedMessage: '',
        secretKey: 'your-secret-key', // Replace with a secure method for key exchange
      };
    },
    methods: {
      handleMessageChange(e) {
        this.message = e.target.value;
      },
      encryptMessage(text) {
        return CryptoJS.AES.encrypt(text, this.secretKey).toString();
      },
      decryptMessage(encryptedText) {
        return CryptoJS.AES.decrypt(encryptedText, this.secretKey).toString(
          CryptoJS.enc.Utf8
        );
      },
      handleSendMessage() {
        const encryptedMessage = this.encryptMessage(this.message);
  
        // Simulate receiving the encrypted message on the other end
        const decryptedMessage = this.decryptMessage(encryptedMessage);
  
        this.encryptedMessage = encryptedMessage;
        this.displayedMessage = decryptedMessage;
        this.message = '';
      },
    },
  };
  </script>
  
  <style scoped>
  /* Add your component-specific styles here */
  </style>
  