<template>
    <h1 class="flex justify-center py-[200px] text-4xl text-[#15393C] font-semibold">Por favor aguarde. Estamos o redirecionando...</h1>
</template>

<script>
import {useAuth0} from "@auth0/auth0-vue";
export default {
    setup() {
        const {loginWithRedirect} = useAuth0();
        return {
            login: () => {
                loginWithRedirect();
            },
        };
    },
    mounted() {
        this.login();
    },
};
</script>

<style></style>
