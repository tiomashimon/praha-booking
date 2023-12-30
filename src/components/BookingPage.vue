<template>
  <div>

    <main class="container my-4">
      <h2>Список кімнат</h2>
      <ul>
        <li v-for="room in rooms" :key="room.id">
          {{ room.name }} - {{ room.price }} грн/ніч
        </li>
      </ul>

      <h2>Додати нову кімнату</h2>
      <form @submit.prevent="addRoom" class="add-room-form">
        <label for="roomName">Назва кімнати:</label>
        <input type="text" id="roomName" v-model="newRoom.name" required>

        <label for="roomPrice">Ціна за ніч:</label>
        <input type="number" id="roomPrice" v-model="newRoom.price" required>

        <button type="submit">Додати кімнату</button>
      </form>
    </main>
  </div>
</template>

<script>
export default {
  data() {
    return {
      rooms: [],
      newRoom: {
        name: '',
        price: 0
      }
    };
  },
  mounted() {
    // Отримати дані про кімнати з локального сховища при завантаженні компонента
    this.rooms = JSON.parse(localStorage.getItem('rooms')) || [];
  },
  methods: {
    addRoom() {
      // Додати нову кімнату до списку та зберегти його в локальному сховищі
      this.rooms.push({ ...this.newRoom, id: Date.now() });
      this.newRoom = { name: '', price: 0 };
      this.saveRoomsToLocalStorage();
    },
    saveRoomsToLocalStorage() {
      localStorage.setItem('rooms', JSON.stringify(this.rooms));
    }
  }
};
</script>

<style scoped>
/* Стилі для сторінки */
header {
  background-color: #007BFF;
}

h1 {
  margin: 0;
}

main {
  text-align: center;
}

ul {
  list-style: none;
  padding: 0;
}

li {
  margin: 10px 0;
}

.add-room-form {
  margin-top: 20px;
}

label {
  display: block;
  margin-bottom: 5px;
}

input {
  width: 100%;
  padding: 8px;
  margin-bottom: 15px;
}

button {
  background-color: #28A745;
  color: white;
  padding: 10px 15px;
  border: none;
  cursor: pointer;
}
</style>
