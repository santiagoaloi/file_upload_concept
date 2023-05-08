<template>
  <VContainer fluid>
    <div>
      <VFileInput
        v-model="data.chosenFile"
        :prepend-icon="null"
        label="Upload a file"
        prepend-inner-icon="$mdiFile"
        variant="solo"
      />

      <VBtn :disabled="!data.chosenFile.length" @click="uploadFile">Upload file</VBtn>
    </div>
  </VContainer>
</template>

<script setup>
import axios from 'axios'

const data = reactive({
  chosenFile: []
})

async function uploadFile() {
  const formData = new FormData()
  formData.append('file', data.chosenFile)

  const response = await axios.post('/api/upload', formData, {
    headers: {
      'Content-Type': 'multipart/form-data'
    }
  })
  console.log(response.data)
}
</script>
