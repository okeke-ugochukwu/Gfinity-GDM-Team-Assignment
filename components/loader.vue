<template>
   <div class="w-full max-w-[300px] bg-black m-auto 
      text-white text-center mt-[100px] py-8 rounded-xl"
      >
      <slot>
         Fetching
      </slot>
   </div>
</template>

<script>
   export default {
      name: 'laoder'
   }
</script>

<style lang="scss" scoped>

</style>