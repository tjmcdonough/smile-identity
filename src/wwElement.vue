<template>
  <div>
    <smart-camera-web>
    </smart-camera-web>
  </div>
</template>

<script>
  import '@smile_identity/smart-camera-web';

  export default {
    data: () => ({
      //......data of component
    }),
    mounted() {
      const app = document.querySelector('smart-camera-web');

  const postContent = async (data) => {

    // Send images to endpoint from data object

    const imagesToSend = [
      //data.images[i].image
    ]

    const options = {
      method: 'POST',
      headers: {
        'Content-Type': 'multipart/form-data',
        'Authorization': 'Bearer {GET_ACCESS_TOKEN_FROM_WEWEB}',
      },
      body: JSON.stringify(imagesToSend)
    };

    try {
      const response = await fetch('https://backend.bnkability.com/api/v1/account/selfies', options);

      if(response.status == 200 || response.status == 201)
      {
        console.log('selfies sent successfully');
        const json = await response.json();
        
        return json;
      }
    } catch (e) {
      console.log('error: selfies sent unsuccessfully');
    }
  };

  app.addEventListener('imagesComputed', async (e) => {

    try {
      const response = await postContent(e.detail);

      console.log(response);
    } catch (e) {
      console.error(e);
    }
  });

    },
    methods: {
      //......methods of component
    }
  }
  
</script>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>
