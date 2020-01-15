<template>
    <div>
        {{ $route.params.lang }}
    </div>
</template>

<script>
export default {
  data: function() {
    return {
      selectedLanguage: this.$route.params.lang,
    }
  }
}
</script>