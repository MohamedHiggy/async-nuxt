<template>
  <header>
    <nav>
      <ul>
        <li class="nav-item">
          <nuxt-link to="/" class="link-tag">Home</nuxt-link>
        </li>
        <li class="nav-item">
          <nuxt-link to="/blogs" class="link-tag">Blogs</nuxt-link>
        </li>
        <li class="nav-item">
          <nuxt-link to="/form" class="link-tag">form</nuxt-link>
        </li>
      </ul>
    </nav>
  </header>
</template>

<script>
export default {}
</script>

<style scoped>

header{
  background-color: #eee;
  padding: 15px 0;
  text-align: center;
}
ul {
  margin: 0;
  padding: 0;
  display: flex;
  justify-content: center;
}
.nav-item{
  color: #000000;
  font-size: 20px;
  list-style: none;
  margin: 0 15px;
}
.nav-item a, .nav-item a:active{
  color: inherit;
  text-decoration: none;
  padding: 4px 10px;
  border-radius: 3px;
}
.nav-item a.nuxt-link-exact-active{
  color: #333;
  border: 1px solid #333333;
}
.link-tag {
  border: 1px solid #eee;
}
</style>
