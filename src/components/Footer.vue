<template>
    <footer>
        <div>
          <router-link to="/"><img alt="logo" src="/assets/TaskMasterLogo.png"></router-link>
          <p>&copy; 2023 Romy Fischer. All rights reserved.</p>
        </div> 
    </footer>
  </template>
  
  <script setup>
  </script>
  
  <style scoped>
  
  footer div {
    color: #0b3142;
    background-color: #c6b9cd;
    width: 100%;
    padding: 0;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
  }

  footer img {
  width: 200px;
  padding-top: 20px;
}

  
  @media (max-width: 980px) {
    footer {
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-content: center;
    }
  }
  
  </style>