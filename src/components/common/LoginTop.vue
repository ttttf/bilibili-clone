<template>
  <div>
      <div class="LoginTop">
          <div></div>
          <div>{{middleTop}}</div>
          <div>
              <slot name="right" />
          </div>
      </div>
  </div>
</template>

<script>
export default {props: ['middleTop']
}
</script>

<style>
.LoginTop{
    height: 12.5vw;
    background-color: white;
    display: flex;
}
.LoginTop div{
        flex: 1;
        display: flex;
        justify-content: center;
        align-items: center;
        font-size: 4.444vw;
}
</style>
