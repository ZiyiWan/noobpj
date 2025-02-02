<template>
  <nav class="navbar" role="navigation" aria-label="Main Navigation">
    <a href="#main-content" class="skip-link">Skip to main content</a>
    <div class="navbar-left">
      <div class="navbar-brand">
        <img src="@/assets/MedicalEmergencySymbol.png" alt="Medical Emergency Symbol" class="navbar-logo" />
        <router-link to="/">MigrantCare</router-link>
      </div>
    </div>
    <ul class="navbar-menu">
      <li><router-link to="/">Home</router-link></li>
      <li v-if="!isAuthenticated"></li>

      <!-- 修复 "Our Services" 的样式 -->
      <li class="dropdown" v-if="isAuthenticated">
        <button aria-haspopup="true" aria-expanded="false" class="dropdown-toggle">
          <router-link to="/service"> Our Services</router-link>
        </button>
        <ul class="dropdown-menu">
          <li><router-link to="/service/language-learning">Language Learning</router-link></li>
          <li><router-link to="/service/career-resources">Career Resources</router-link></li>
          <li><router-link to="/service/health-info">Health Information</router-link></li>
          <li>
            <router-link to="/service/cultural-integration">Cultural Integration</router-link>
          </li>
        </ul>
      </li>

      <li><router-link to="/admin" v-if="role === 'admin'">Admin Panel View Page</router-link></li>
      <li><router-link to="/review" v-if="isAuthenticated">Review</router-link></li>
      <li><router-link to="/events" v-if="isAuthenticated">Events</router-link></li>
      <li><router-link to="/about">About us</router-link></li>
      <li><router-link to="/askus">Ask us</router-link></li>
      <li><router-link to="/contactus">Contact us</router-link></li>
    </ul>
    <div class="navbar-right">
      <div v-if="!isAuthenticated" class="ml-3"><router-link to="/login"><Button label="Log in" severity="secondary"
            raised /></router-link></div>
      <div v-if="isAuthenticated">
        <SplitButton :model="items" severity="secondary">Login as {{ role }}</SplitButton>
      </div>
    </div>

  </nav>
</template>

<script setup>
import { useRouter } from 'vue-router'
import { role, isAuthenticated } from '../router/index.js'
import Button from 'primevue/button';
import SplitButton from 'primevue/splitbutton';
const router = useRouter()
const items = [
  {
    label: 'Logout',
    command: () => {
      role.value = ''
      isAuthenticated.value = false
      router.push('/')
    }
  }
];


</script>

<style scoped>
/* 导航栏样式 */
.navbar {
  background-color: #0074cc;
  padding: 15px 30px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  position: relative;
}

.skip-link {
  position: absolute;
  left: -999px;
  top: -999px;
}

.skip-link:focus {
  position: static;
  background-color: #ffcc33;
  padding: 10px;
  color: black;
  z-index: 1000;
}

/* 品牌样式 */
.navbar-left {
  display: flex;
  align-items: center;
}

.navbar-brand {
  display: flex;
  align-items: center;
}

.navbar-brand img.navbar-logo {
  width: 40px;
  height: 40px;
  margin-right: 10px;
}

.navbar-brand a {
  color: white;
  font-size: 24px;
  text-decoration: none;
}

/* 导航菜单样式 */
.navbar-menu {
  list-style: none;
  display: flex;
  margin: 0;
  padding: 0;
  flex-grow: 1;
  /* 让菜单占据中间位置 */
  justify-content: center;
  /* 确保导航菜单居中 */
}

.navbar-menu li {
  margin-right: 20px;
  position: relative;
}

.navbar-menu li a {
  color: white;
  text-decoration: none;
}

.navbar-menu li a:focus {
  outline: 3px solid #ffcc33;
}

.navbar-menu li a:hover {
  color: #ffcc33;
}

/* 修复 "Our Services" 样式 */
.dropdown {
  display: flex;
  align-items: center;
  justify-content: center;
}

.dropdown-toggle {
  background: none;
  border: none;
  color: white;
  cursor: pointer;
  font-size: 16px;
  line-height: 24px;
  text-align: center;
}

.dropdown-menu {
  display: none;
  position: absolute;
  top: 100%;
  left: 0;
  background-color: #0074cc;
  list-style: none;
  padding: 0;
  margin: 0;
  z-index: 1000;
}

.dropdown-menu li {
  padding: 10px 20px;
  white-space: nowrap;
  text-align: center;
  /* Center-aligns the text */
}

.dropdown:hover .dropdown-menu {
  display: block;
}

.dropdown-menu li a {
  color: white;
  text-decoration: none;
}

.dropdown-menu li a:focus {
  outline: 3px solid #ffcc33;
}

.dropdown-menu li a:hover {
  color: #ffcc33;
}

/* 搜索和用户部分 */
.navbar-right {
  display: flex;
  align-items: center;
  color: white;
}

.navbar-right input {
  padding: 5px;
  margin-right: 10px;
  border-radius: 5px;
  border: 1px solid #ccc;
}

.navbar-right input:focus {
  outline: 3px solid #ffcc33;
}

.navbar-right button {
  padding: 5px 10px;
  background-color: #ffcc33;
  border: none;
  border-radius: 5px;
  color: black;
  cursor: pointer;
}

.navbar-right button:hover {
  background-color: #ff9933;
}

/* 用户下拉菜单样式 */
.user-dropdown {
  position: relative;
  margin-left: 20px;
  color: white;
  cursor: pointer;
}

.user-dropdown button {
  background: none;
  border: none;
  color: white;
  cursor: pointer;
}

.user-dropdown button:focus {
  outline: 3px solid #ffcc33;
}

.user-dropdown-menu {
  display: none;
  position: absolute;
  top: 100%;
  right: 0;
  background-color: #0074cc;
  list-style: none;
  padding: 0;
  margin: 0;
}

.user-dropdown:hover .user-dropdown-menu {
  display: block;
}

.user-dropdown-menu li {
  padding: 10px 20px;
}

.user-dropdown-menu li:focus {
  outline: 3px solid #ffcc33;
}

.user-dropdown-menu li:hover {
  background-color: #0056b3;
}
</style>
