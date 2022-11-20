<template>
    <div class="footer">
      <div class="wrapper">
          <div>The_viscount</div>
          <div> Copyright</div>
          <div>&copy;2022</div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
  name: 'Footer'
  }
  </script>
  
  <style scoped>
      .footer{
          bottom: 0;
          position: sticky;
          height: auto;
          width: 100%;
          background: #647E68;
          color: #fff;
      }
      .wrapper{
          display: flex;
          flex-direction: column;
          align-content: center;
          justify-content: center;
          justify-items: center;
          margin: 0 auto;
          width: max-content;
      }
      
  </style>