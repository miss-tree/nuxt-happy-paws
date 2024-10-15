<script setup lang="ts">
  const { navlinks, navlinksPrimary, navlinksSecondary, currentPath } = useNav()
  const { locale } = useI18n()
  const state = useState("state",()=>{
    return {
      navlinks,navlinksPrimary, navlinksSecondary
    }
  })
  onMounted(() => {
    watch(locale, (n,o) => {
      if(n){
        state.value.navlinks = useNav().navlinks
        state.value.navlinksPrimary = useNav().navlinksPrimary
        state.value.navlinksSecondary = useNav().navlinksSecondary
      }
    })
  })
</script>

<template>
  <div class="w-full">
    <nav class>
      <div class="container mx-auto px-4 sm:px-6">
        <div class="flex h-24 items-center justify-between">
          <div class="flex items-center justify-between w-full">
            <div class="flex flex-shrink-0 items-center">
              <TheLogo />
            </div>
            <NavPrimary
              :navlinks="state.navlinksPrimary"
              :current-path="currentPath"
              class="hidden sm:flex sm:ml-6"
            />
          </div>
          <DarkModeSwitch />
          <div class="-mr-2 items-center relative">
            <NavHamburger
              v-if="state.navlinksSecondary.length"
              class="hidden sm:block"
            />
            <NavHamburger v-if="state.navlinks.length" class="sm:hidden" />
            <NavSecondary
              class="hidden sm:flex sm:justify-end absolute right-0 mt-4"
              :navlinks="state.navlinksSecondary"
              :current-path="currentPath"
            />
          </div>
        </div>
      </div>
      <NavSecondary
        class="sm:hidden"
        :navlinks="state.navlinks"
        :current-path="currentPath"
      />
    </nav>
  </div>
</template>

<style scoped></style>
