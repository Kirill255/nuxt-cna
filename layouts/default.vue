<template>
  <section class="is-primary is-medium">
    <!-- Hero head: will stick at the top -->
    <div class="head">
      <nav class="navbar">
        <div class="container">
          <div class="navbar-menu">
            <div class="navbar">
              <nuxt-link class="navbar-item"
                         :to="{path: '/'}"
                         exact>Home</nuxt-link>

              <nuxt-link class="navbar-item"
                         :to="{path: '/about'}">About</nuxt-link>

              <nuxt-link class="navbar-item"
                         :to="{path: '/user'}">User</nuxt-link>

              <nuxt-link class="navbar-item"
                         :to="{path: '/editor'}">Editor</nuxt-link>

            </div>
          </div>
        </div>
      </nav>
    </div>

    <!-- Hero content: will be in the middle -->
    <div class="body">
      <div class="container has-text-centered">
        <nuxt/>
      </div>
    </div>

    <!-- Hero footer: will stick at the bottom -->
    <div class="footer">
      <div class="container">
        Footer
      </div>
    </div>
  </section>
</template>



<style>
</style>
