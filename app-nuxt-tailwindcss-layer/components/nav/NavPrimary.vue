<script setup lang="ts">
  defineProps({
    navlinks: {
      type: Object,
      default() {
        return []
      },
    },
    currentPath: {
      type: String,
      default: '/',
    },
  })
  const { locale,setLocale } = useI18n()
  const state = reactive({
    switchLabel :locale.value=='zh'?'English':'中文'
  })
  const changeLanguage = ()=>{
    if(locale.value=='zh'){
        setLocale('en')
        state.switchLabel = '中文'
    }else{
        setLocale('zh')
        state.switchLabel = 'English'
    }
  }
</script>

<template>
  <div class="h-full items-center">
    <div class="flex h-full space-x-2">
      <BaseButton
        v-for="(navlink, index) in navlinks"
        :key="index"
        :to="navlink.link"
        :label="navlink.text"
        size="lg"
        :variant="isCurrentRoute(navlink, currentPath) ? 'solid' : 'ghost'"
        class="!rounded-lg"
      />
    </div>
    <BaseButton
      class="ml-3 py2"
      size="xl"
      color="secondary"
      @click="changeLanguage"
    >
      <span class="px-2">{{state.switchLabel}}</span>
    </BaseButton>
  </div>
</template>

<style scoped></style>
