<template>
    <div class="flex content-center fixed inset-0 bg-gray-100">
        <div class="bg-white border m-auto p-10 rounded shadow-lg space-y-6  w-1/4">
            <div class="flex items-center mb-5">
                <h1 class="font-semibold text-3xl  text-yellow-600 flex-grow ">
                    Area Membros
                </h1>
                <p @click="sair()" class="cursor-pointer">Sair</p>
            </div>
            <hr />

            <p class="font-semibold mb-3 text-gray-400">
                Cursos Disponíveis &#8628;
            </p>

            <ul class="text-lg space-y-4 text-gray-700 font-semibold">
                <li v-for="curso in cursos" class="hover:text-yellow-900 cursor-pointer">{{ curso.titulo }}</li>
            </ul>
        </div>
    </div>
</template>
<script>
export default {
    data() {
        return {
            cursos: [],
        };
    },
    created() {
        this.carregarCursos();
    },
    middleware: "auth",
    methods: {
        carregarCursos: function () {
            this.$axios
                .$get("cursos")
                .then((res) => {
                    this.cursos = res.data;
                })
                .catch((error) => {
                    console.error(error);
                });
        },
        async sair() {
            await this.$auth.logout();
        },
    },
};
</script>