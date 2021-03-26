<template>
    <div class="container mx-auto my-20">
        <h1 class="font-semibold text-3xl">Area Membros</h1>
        <p class="my-10">Cursos Disponíveis</p>

        <ul class="text-lg space-y-4 italic">
            <li v-for="curso in cursos">{{ curso.titulo }}</li>
        </ul>
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
    },
};
</script>