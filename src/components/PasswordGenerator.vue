<template>
  <div class="generator-container">
    <h3>Generator hasła</h3>
    <div class="result-container">
      <input v-model="password" type="text" readonly placeholder="Wygeneruj hasło">
      <button :disabled="!password.length" class="btn" @click="copyToClipboard">&#x2398;</button>
    </div>
    <div class="settings">
      <div class="password-length">
        <label for="length">Długość hasła</label>
        <input type="number" v-model="length" min="7" max="100">
      </div>
      <div class="options">
        <div class="option">
          <label>Duże litery</label>
          <input type="checkbox" v-model="uppercase">
        </div>
        <div class="option">
          <label>Małe litery</label>
          <input type="checkbox" v-model="lowercase">
        </div>
        <div class="option">
          <label>Liczby</label>
          <input type="checkbox" v-model="numbers">
        </div>
        <div class="option">
          <label>Symbole</label>
          <input type="checkbox" v-model="symbols">
        </div>
        <div class="option">
          <label>Polskie litery</label>
          <input type="checkbox" v-model="polishChars">
        </div>
      </div>
      <button :disabled="!uppercase && !lowercase && !numbers && !numbers && !symbols && !polishChars" 
              @click="generatePassword" class="btn generate">Wygeneruj hasło</button>
    </div>
  </div>
</template>

<script>
import { toast } from 'vue3-toastify';
import 'vue3-toastify/dist/index.css';
export default {
  data() {
    return {
      password: "",
      length: 14,
      uppercase: true,
      lowercase: true,
      numbers: true,
      symbols: true,
      polishChars: false
    };
  },
  methods: {
    generatePassword() {
      const upperChars = "QWERTYUIOPASDFGHJKLZXCVBNM";
      const lowerChars = "qwertyuiopasdfghjklzxcvbnm";
      const numbers = "0123456789";
      const symbolChars = "!@#$%^&*(){}[].,:<>?";
      const polishUpperChars = "ŻŹĆŃŁÓŚ";
      const polishLowerChars = "żźćńłóś";

      let allChars = "";

      if (this.uppercase) allChars += upperChars;
      if (this.lowercase) allChars += lowerChars;
      if (this.numbers) allChars += numbers;
      if (this.symbols) allChars += symbolChars;
      if (this.uppercase && this.polishChars) allChars += polishUpperChars;
      if (this.lowercase && this.polishChars) allChars += polishLowerChars;

      if (allChars === "") return;

      let password = "";

      for (let i = 0; i < this.length; i++) {
        const randomIndex = Math.floor(Math.random() * allChars.length);

        password += allChars[randomIndex];
      }

      this.password = password;
    },
    copyToClipboard() {
      navigator.clipboard.writeText(this.password).then(() => {
        console.log("Hasło skopowano do schowka");
        toast("Hasło skopowano do schowka", {
          autoClose: 1000,
          position: "bottom-right",
          theme: "colored",
          type: "success"
        });
      });
    }
  }
}

</script>

<style>
  .generator-container {
    padding: 20px;
    width: 360px;
    background-color: #41b884;
    color: white;
    box-shadow: 0px 10px 12px rgba(0, 0, 0, 0.3);
  }
  
  h3 {
    margin-bottom: 20px;
    text-align: center;
  }
  
  .result-container {
    display: flex;
    justify-content: space-between;
    align-items: center;
    height: 45px;
    margin-bottom: 22px;
    font-size: 16px;
  }
  
  .result-container input {
    width: 85%;
    padding: 10px;
    border: none;
    border-radius: 5px;
  }
  
  .btn {
    background-color: #0993fd;
    border: none;
    padding: 10px;
    color: #fff;
    border-radius: 5px;
    cursor: pointer;
  }
  
  .result-container .btn {
    width: 30px;
    padding: 3px;
    font-size: 24px;
    background-color: #fdc009;
    color: #000;
  }
  
  .result-container .btn:hover {
    filter: brightness(1.1);
  }
  
  button.generate {
    width: 100%;
    font-weight: bold;
  }
  
  button.generate:hover {
    filter: brightness(1.2);
  }
  
  .settings {
    margin-bottom: 20px;
  }
  
  .password-length {
    display: flex;
    justify-content: space-between;
    margin-bottom: 12px;
  }
  
  .options {
    display: grid;
    grid-template-columns: 1fr 1fr;
    column-gap: 50px;
    margin-bottom: 12px;
  }
  
  .option {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin: 5px 0;
  }
  .btn:disabled{
    opacity: 0.8;
  }
</style>