<template>
  <div>
    <h1>Transcription Audio</h1>
    <input type="file" @change="onFileChange" />
    <button @click="uploadFile">Transcrire</button>
    <p v-if="transcript">{{ transcript }}</p>
  </div>
</template>
<script>
import axios from 'axios';
export default {
  name: 'UploadFile',
  data() {
    return {
      file: null,
      transcript: '',
    };
  },
  methods: {
    onFileChange(event) {
      this.file = event.target.files[0];
    },
    async uploadFile() {
      const formData = new FormData();
      formData.append('file', this.file);
      try {
        const response = await axios.post('http://localhost:3000/transcription', formData, {
          headers: {
            'Content-Type': 'multipart/form-data',
          },
        });
        this.transcript = response.data;
      } catch (error) {
        console.error(error);
      }
    },
  },
};
</script>