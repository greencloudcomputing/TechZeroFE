<template>
    <div class="item">
      <div class="details">
        <h3>
          <slot name="heading"></slot>
        </h3>
        <slot></slot>
      </div>
    </div>
</template>
  
  <style scoped>
  /* .item {
    margin-top: 2rem;
    display: flex;
    position: relative;
  } */

  .item {
    background-color: white;
    border-radius: 10px;
    margin: 10px;
    padding: 10px;
  }
  
  .details {
    flex: 1;
    margin-left: 1rem;
    /* color: white; */
  }
  
  h3 {
    font-size: 1.2rem;
    font-weight: 500;
    margin-bottom: 0.4rem;
    /* color: white; */
  }
  
  /* @media (min-width: 1024px) {
    .item {
      margin-top: 0;
      padding: 0.4rem 0 1rem calc(var(--section-gap) / 2);
    }
  } */
  </style>