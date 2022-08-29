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
      //......data of your component
    }),
    mounted() {
      const app = document.querySelector('smart-camera-web');

  const postContent = async (data) => {

    const imagesToSend = {
      'image-one': data.images[0].image,
      'image-two': data.images[1].image,
      'image-three': data.images[2].image,
      'image-four': data.images[3].image,
      'image-five': data.images[4].image,
      'image-six': data.images[5].image,
      'image-seven': data.images[6].image,
    }

    const options = {
      method: 'POST',
      headers: {
        'Content-Type': 'multipart/form-data',
        'Authorization': 'Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNjYxODM0Nzc3LCJpYXQiOjE2NjE3NDgzNzcsImp0aSI6ImUxYzQ5ZDM3ZDhlYjQ2MjRhM2JmNGY5MTk5ZTdiZTNjIiwidXNlcl9pZCI6IjIxOWM4M2VjLWRmNjktNGQzOS1hYWQyLTlmODg4YzgwYTA4OSJ9.1G1CfgWAr8G3HNJcjYbXZ0NFOxpeJi_cZyKbcW3y0zw',
      },
      body: JSON.stringify(imagesToSend)
    };

    try {
      const response = await fetch('http://bnkability-staging-001.eu-west-2.elasticbeanstalk.com/api/v1/account/selfies', options);

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
      //......methods of your component
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
