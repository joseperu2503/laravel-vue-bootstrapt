<template>
    <div class="container">
        <div class="row">
            <div class="col-12">
                <div class="card">
                    <div class="card-header"><h4>Editar Blog</h4></div>
                    <div class="card-body">
                        <form @submit.prevent="actualizar">
                            <div class="mb-3">
                                <label class="form-label">Título</label>
                                <input type="text" class="form-control" v-model="blog.titulo">
                            </div>
                            <div class="mb-3">
                                <label class="form-label">Contenido</label>
                                <textarea class="form-control" rows="3" v-model="blog.contenido"></textarea>
                            </div>
                            <button type="submit" class="btn btn-success">Guardar</button>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    name:"editar-blog",
    data(){
        return{
            blog:{
                titulo:"",
                contenido:""
            }
        }
    },
    mounted(){
        this.mostrarBlog()
    },
    methods:{
        async mostrarBlog(){
            this.axios.get(`/api/blog/${this.$route.params.id}`)
            .then(response=>{
                const {titulo,contenido} = response.data
                this.blog.titulo = titulo
                this.blog.contenido = contenido
            })
            .catch(error=>{
                console.log(error)
            })
        },
        actualizar(){
            this.axios.put(`/api/blog/${this.$route.params.id}`,this.blog)
            .then(response=>{
                this.$router.push({name:"mostrarBlogs"})
            })
            .catch(error=>{
                console.log(error)
            })
        }
    }
}
</script>