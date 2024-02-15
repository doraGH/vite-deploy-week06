<template>
  <h2>前台</h2>
  <nav>
    <RouterLink to="/">首頁</RouterLink> |
    <RouterLink to="/about">關於我們</RouterLink> |
    <RouterLink to="/products">前台產品列表</RouterLink> |
    <RouterLink to="/cart">購物車</RouterLink> |
    <RouterLink to="/login">登入頁</RouterLink> |
    <RouterLink to="/admin/products">後台購物車列表</RouterLink>
  </nav>
  <RouterView></RouterView>
</template>
