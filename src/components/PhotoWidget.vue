<template>
  <div class="photo-widget">
    <h2>Random Photo</h2>
    <div class="photo-container">
      <img :src="photoUrl" :alt="photoDescription" />
      <button @click="getRandomPhoto">Get Random Photo</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      photoUrl: '',
      photoDescription: '',
      apiKey: '38037020-2c48722c03be8437a05b588e6',
    };
  },
  mounted() {
    this.getRandomPhoto();
  },
  methods: {
    async getRandomPhoto() {
      try {
        const apiUrl = `https://pixabay.com/api/?key=${this.apiKey}&q=nature&image_type=photo&orientation=horizontal`;

        const response = await fetch(apiUrl);
        const data = await response.json();

        const randomIndex = Math.floor(Math.random() * data.hits.length);
        this.photoUrl = data.hits[randomIndex].webformatURL;
        this.photoDescription = data.hits[randomIndex].tags;
      } catch (error) {
        console.error(error);
      }
    },
  },
};
</script>

<style scoped>
.photo-widget {
  text-align: center;
}

.photo-container {
  margin-top: 20px;
}

.photo-container img {
  max-width: 500px;
}

button {
  margin-top: 10px;
  background-color: #4caf50;
  color: #fff;
  border: none;
  padding: 8px 16px;
  font-size: 16px;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #45a049;
}
</style>
