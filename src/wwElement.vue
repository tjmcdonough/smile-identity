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

      const images = data.images.map(function(item) {
        return item['image'];
      });

      const imageArray = {
        "images": images
      }

      const options = {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
          // Need to add authorization header here
          'Authorization': 'Bearer ' + this.content.accessToken
        },
        body: JSON.stringify(imageArray)
      };

        // Should be able to get base uri `https://backend.bnkability.com/api/v1` from we web variables 
        const response = await fetch('https://backend.bnkability.com/api/v1/account/selfies', options);

        if(response.status == 200 || response.status == 201)
        {
          console.log('selfies sent successfully');

          // Need to return a property here so we know it is successful

          const json = await response.json();
          
          return json;
        }
        else {
          console.log('error: selfies sent unsuccessfully');
        }
    };

    app.addEventListener('imagesComputed', async (e) => {

    const response = await postContent(e.detail);

    console.log(response);
     
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
