<template>
    <header class="header">
      <div class="content-container">
        <h1>
            <slot name="heading"></slot>
        </h1>
        <slot></slot>
      </div>
      <div class="logo-container">
        <img src="@/assets/greencloudlogo.png" alt="Logo" class="logo" />
      </div>
    </header>
  </template>

<script>
export default {
  name: 'AppHeader',
 
};
</script>
  
  <style>
  .header {
    display: flex;
    align-items: center;
    background-color: #333;
    color: #fff;
    padding: 0.5rem 2rem;
    justify-content: space-between;
  }

  .heading {
    margin: 0; /* Remove default margin */
    /* Additional styling for the title */
  }
  
  .logo-container {
    /* position: right; */
  }
  
  .logo {
    padding-left: 50rem;
    height: 50px;
    width: auto;
  }

  </style>