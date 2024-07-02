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
  
  <style>
  /* Basic header styles */
  .header {
    display: flex;
    align-items: center;
    background-color: #333;
    color: #fff;
    padding: 0.5rem 2rem;
    justify-content: space-between;
  }
  
  .logo-container {
    /* position: right; */
  }

  .content-container {
    flex-grow: 1;
  }
  
  .logo {
    height: 50px;
    width: auto;
  }

  </style>