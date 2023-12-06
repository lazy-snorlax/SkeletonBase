<template>
    <div id="sidebar-wrapper" :class="`${is_expanded ? 'is-expanded' : ''}`">
        <div class="logo">
            <img :src="logo" alt="LOGO.png">
        </div>

        <div class="menu-toggle-wrap">
            <button class="menu-toggle" @click="toggleMenu">
				<font-awesome-icon icon="fa-solid fa-bars"></font-awesome-icon>
            </button>
        </div>

        <h3>Menu</h3>

		<!-- First Menu Grouping -->
        <div class="menu">
            <router-link :to="{ name: 'dashboard' }" class="button">
				<font-awesome-icon icon="fa-solid fa-table-columns"></font-awesome-icon>
				<span class="text">Dashboard</span>
            </router-link>
			<div v-if="loggedInUser">
				<router-link 
					class="button" 
					:to="{ name:'my-account' }" 
					:class="{ 'router-link-exact-active': $route.name.toString().includes('my-account') }">
					<font-awesome-icon icon="fa-solid fa-user"></font-awesome-icon> <span class="text">My Account</span>
				</router-link>
			</div>
        </div>
		
		<!-- Second Menu Grouping -->
        <div class="menu flex">
		</div>

		<!-- Footer Menu Grouping -->
        <div class="menu">
			<a class="button" @click="logout" v-if="loggedInUser">
				<font-awesome-icon icon="fa-solid fa-user"></font-awesome-icon> <span class="text">Logout</span>
			</a>
			<router-link 
				v-else
				class="button" 
				:to="{ name:'login' }" 
				>
                <font-awesome-icon icon="fa-solid fa-user"></font-awesome-icon> <span class="text">Login</span>
            </router-link>
        </div>

    </div>
</template>

<script lang="ts" setup>
import { ref, computed } from 'vue'
import logoDefault from '@/assets/logo.svg'
import { useLogout } from '../../composables/use-logout'
import { useLoggedInUser } from '../../composables/use-logged-in-user'

const is_expanded = ref(localStorage.getItem("is_expanded") === "true")
const toggleMenu = () => {
    is_expanded.value = !is_expanded.value
    localStorage.setItem("is_expanded", is_expanded.value)
}

const logo = computed(() => {
	return logoDefault
})

const { logout } = useLogout();
const { loggedInUser } = useLoggedInUser();

</script>