<template>
    <div id="AuthPage" class="w-full h-[100vh] bg-white">
        <div class="w-full flex items-center justify-center p-5 border-b border-b-gray-300">
            <NuxtLink to="/" class="min-w-[170px]">
                <img width="170" src="/logo-final.png">
            </NuxtLink>
        </div>

        <div class="max-w-[400px] mx-auto px-2">

            <div class="text-center my-6 font-semibold text-lg">Login / Register</div>
            <div class="text-center my-6 font-semibold text-lg">Discover our shop with tons of cat things!</div>
            <img class="mx-auto rounded-sm mb-4" src="/cat-line.jpg">

            <button @click="login('google')" class="
                    flex 
                    items-center 
                    justify-center 
                    gap-3
                    p-1.5
                    w-full 
                    border 
                    hover:bg-gray-200
                    rounded-full
                    text-lg
                    font-semibold
                ">
                <img class="w-full max-w-[30px]" src="/google-logo.png">
                <div>Login with Google</div>
            </button>

            <button @click="login('github')" class="
                mt-4
                    flex 
                    items-center 
                    justify-center 
                    gap-3
                    p-1.5
                    w-full 
                    border 
                    hover:bg-gray-200
                    rounded-full
                    text-lg
                    font-semibold
                ">
                <img class="w-full max-w-[30px]" src="/github-logo.png">
                <div>Login with Github</div>
            </button>

        </div>
    </div>
</template>

<script setup>
const client = useSupabaseClient()
const user = useSupabaseUser()

watchEffect(() => {
    if (user.value) {
        return navigateTo('/')
    }
})

const login = async (prov) => {
    const { data, error } = await client.auth.signInWithOAuth({
        provider: prov,
        redirectTo: window.location.origin
    })
}
</script>
