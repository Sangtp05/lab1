<template>
    <div class="profile-card">
      <img :src="imageUrl" alt="Profile Picture" class="profile-img" />
      <h2>{{ name }}</h2>
      <p>{{ description }}</p>
  
      <h3>Sở Thích:</h3>
      <ul>
        <li v-for="hobby in hobbies" :key="hobby">{{ hobby }}</li>
      </ul>
  
      <button @click="updateInfo" class="edit-btn">Edit</button>
    </div>
  </template>
  
  <script>
  export default {
    name: "HelloWorld",
    props: {
      imageUrl: {
        type: String,
        default: "https://cdn.tuoitre.vn/thumb_w/730/471584752817336320/2024/10/20/37655133-1729441009310281039725.jpg"
      },
      name: {
        type: String,
        default: "Trần Phú Sang"
      },
      description: {
        type: String,
        default: "Giới thiệu bản thân"
      },
      hobbies: {
        type: Array,
        default: () => ["Đọc sách", "Chơi thể thao", "Du lịch"]
      }
    },
    methods: {
      updateInfo() {
        // Logic cập nhật thông tin
        console.log("Updating info...");
      }
    }
  };
  </script>
  
  <style scoped>
  .profile-card {
    border: 1px solid #ddd;
    border-radius: 8px;
    padding: 20px;
    text-align: center;
    width: 300px;
    font-family: Arial, sans-serif;
    color: #070000;
  }
  .profile-img {
    width: 100%;
    border-radius: 8px;
    margin-bottom: 10px;
  }
  .edit-btn {
    background-color: #6c63ff;
    color: #010000;
    border: none;
    border-radius: 4px;
    padding: 8px 16px;
    cursor: pointer;
  }
  .edit-btn:hover {
    background-color: #5a52d6;
  }
  </style>