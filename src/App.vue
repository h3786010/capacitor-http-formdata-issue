<template>
  <div>
    <input type="file" name="file" id="file">
    <br>
    <input type="button" value="upload" @click="upload">
  </div>
</template>

<script setup>
import { CapacitorHttp } from '@capacitor/core'

const upload = async() => {

  const formData = new FormData()
  formData.append('file', document.getElementById('file').files[0])

  await CapacitorHttp.post({
    url: 'https://domain.com/',
    headers: {
      "Content-Type": 'multipart/form-data',
    },
    dataType: 'formData',
    data: formData,
    webFetchExtra: {
      credentials: "include",
    },
  }).then((response) => {
    alert(response.status)
  }).catch((error) => {
    alert(error.message)
  })

}

</script>