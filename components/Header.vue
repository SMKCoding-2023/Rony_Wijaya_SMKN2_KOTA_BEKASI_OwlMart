<script lang="ts" setup>
import { useAuthStore } from '~/stores/auth';
const authStore = useAuthStore();
const isAuthenticated = ref();
const router = useRouter();

isAuthenticated.value = useCookie('access_token').value;

const logout = async () => {
  await authStore.logout();
  const accessToken = useCookie('access_token');
  const refreshToken = useCookie('refresh_token');
  accessToken.value = null;
  refreshToken.value = null;
  setTimeout(() => {
    isAuthenticated.value = useCookie('access_token').value;
  }, 100);
  router.push({
    path: '/',
  });
};
</script>

<template>
  <!-- Main navigation container -->
  <nav
    class="flex-no-wrap relative flex w-full items-center justify-between bg-[#FBFBFB] py-2 shadow-md shadow-black/5 dark:bg-neutral-600 dark:shadow-black/10 lg:flex-wrap lg:justify-start lg:py-4"
  >
    <div class="flex w-full flex-wrap items-center justify-between px-3">
      <!-- Hamburger button for mobile view -->
      <button
        class="block border-0 bg-transparent px-2 text-neutral-500 hover:no-underline hover:shadow-none focus:no-underline focus:shadow-none focus:outline-none focus:ring-0 dark:text-neutral-200 lg:hidden"
        type="button"
        data-te-collapse-init
        data-te-target="#navbarSupportedContent12"
        aria-controls="navbarSupportedContent12"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <!-- Hamburger icon -->
        <span class="[&>svg]:w-7">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            viewBox="0 0 24 24"
            fill="currentColor"
            class="h-7 w-7"
          >
            <path
              fill-rule="evenodd"
              d="M3 6.75A.75.75 0 013.75 6h16.5a.75.75 0 010 1.5H3.75A.75.75 0 013 6.75zM3 12a.75.75 0 01.75-.75h16.5a.75.75 0 010 1.5H3.75A.75.75 0 013 12zm0 5.25a.75.75 0 01.75-.75h16.5a.75.75 0 010 1.5H3.75a.75.75 0 01-.75-.75z"
              clip-rule="evenodd"
            />
          </svg>
        </span>
      </button>

      <!-- Collapsible navigation container -->
      <div
        class="!visible hidden flex-grow basis-[100%] items-center lg:!flex lg:basis-auto"
        id="navbarSupportedContent12"
        data-te-collapse-item
      >
        <!-- Logo -->
        <img
          src="../public/images/icons/images.png"
          style="height: 50px"
          alt="TE Logo"
          loading="lazy"
        />
        <!-- Left navigation links -->
        <ul class="list-style-none mr-auto flex flex-col pl-0 lg:flex-row" data-te-navbar-nav-ref>
          <li class="mb-4 lg:mb-0 lg:pr-2 mt-2" data-te-nav-item-ref>
            <nuxt-link
              to="/Product"
              class="text-neutral-500 transition duration-200 hover:text-neutral-700 hover:ease-in-out focus:text-neutral-700 disabled:text-black/30 motion-reduce:transition-none dark:text-neutral-200 dark:hover:text-neutral-300 dark:focus:text-neutral-300 lg:px-2 [&.active]:text-black/90 dark:[&.active]:text-zinc-400"
              >Home</nuxt-link
            >
          </li>
          <!-- Team link -->
          <li class="mb-4 lg:mb-0 lg:pr-2 mt-2" data-te-nav-item-ref>
            <nuxt-link
              to="/cart"
              class="text-neutral-500 transition duration-200 hover:text-neutral-700 hover:ease-in-out focus:text-neutral-700 disabled:text-black/30 motion-reduce:transition-none dark:text-neutral-200 dark:hover:text-neutral-300 dark:focus:text-neutral-300 lg:px-2 [&.active]:text-black/90 dark:[&.active]:text-neutral-400"
              >Cart</nuxt-link
            >
          </li>
          <li class="mb-4 lg:mb-0 lg:pr-2 mt-2" data-te-nav-item-ref>
            <nuxt-link
              to="/products"
              class="text-neutral-500 transition duration-200 hover:text-neutral-700 hover:ease-in-out focus:text-neutral-700 disabled:text-black/30 motion-reduce:transition-none dark:text-neutral-200 dark:hover:text-neutral-300 dark:focus:text-neutral-300 lg:px-2 [&.active]:text-black/90 dark:[&.active]:text-neutral-400"
              >Product</nuxt-link
            >
          </li>
          <!-- Projects link -->
          <!-- <li class="mb-4 lg:mb-0 lg:pr-2 mt-2" data-te-nav-item-ref>
            <nuxt-link
              to="/products"
              class="text-neutral-500 transition duration-200 hover:text-neutral-700 hover:ease-in-out focus:text-neutral-700 disabled:text-black/30 motion-reduce:transition-none dark:text-neutral-200 dark:hover:text-neutral-300 dark:focus:text-neutral-300 lg:px-2 [&.active]:text-black/90 dark:[&.active]:text-neutral-400"
              >Product</nuxt-link
            >
          </li> -->
          <li class="mb-4 lg:mb-0 lg:pr-2 mt-2" data-te-nav-item-ref>
            <NuxtLink
              to="/login"
              class="text-base bg-blue-600 px-6 py-2 text-white rounded-lg hover:bg-blue-600/80"
              style="margin-left: 1100px"
              >Login</NuxtLink
            >
          </li>
          <li class="mb-4 lg:mb-0 lg:pr-2" data-te-nav-item-ref>
            <NuxtLink
              v-if="!isAuthenticated"
              to="/login"
              class="text-base bg-blue-600 px-6 py-2 text-white rounded-lg hover:bg-blue-600/80"
              >Login</NuxtLink
            >
            <div
              to="/login"
              v-else
              class="text-base cursor-pointer bg-red-600 px-6 py-2 text-white rounded-lg hover:bg-red-600/80"
              @click="logout"
            >
              Logout
            </div>
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>
