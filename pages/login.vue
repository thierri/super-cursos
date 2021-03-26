<template>
    <div class="flex content-center fixed inset-0 bg-gray-100">
        <form
            @submit.prevent="userLogin"
            class="bg-white border m-auto p-10 rounded shadow-lg space-y-6"
        >
            <div class="flex items-center mb-5">
                <h1 class="font-semibold text-3xl text-yellow-600 flex-grow">
                    Entrar na sua conta
                </h1>
            </div>
            <hr />
            <div>
                <label class="block mb-2 font-semibold text-gray-600"
                    >Usuário</label
                >
                <input
                    class="border p-2 w-full"
                    type="text"
                    v-model="login.username"
                />
            </div>
            <div>
                <label class="block mb-2 font-semibold text-gray-600"
                    >Senha</label
                >
                <input
                    class="border p-2 w-full"
                    type="text"
                    v-model="login.password"
                />
            </div>

            <div class="bg-red-100 text-red-600 p-5" v-if="error">
                Ops, algo errado. Tente novamente.
            </div>

            <button class="p-2 w-full bg-yellow-600 text-white" type="submit">
                Entrar
            </button>
        </form>
    </div>
</template>

<script>
export default {
    data() {
        return {
            login: {
                username: "",
                password: "",
            },
            error: false
        };
    },
    created() {
        if (this.$auth.loggedIn) {
            this.$router.push("area-membros");
        }
    },
    methods: {
        async userLogin() {
            this.error = false;
            try {
                let response = await this.$auth.loginWith("local", {
                    data: this.login,
                });
                console.log("Sucesso!");
                console.log(response);
            } catch (err) {
                this.error = true;
                console.log(err);
            }
        },
    },
};
</script>