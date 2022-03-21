<template>
    <div class="container">
        <div class="row">
            <div class="col-12">
                <div class="card">
                    <div class="card-header"><h4>Crear Blog</h4></div>
                    <div class="card-body">
                        <form @submit.prevent="crear">
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
    name:"crear-blog",
    data(){
        return{
            blog:{
                titulo:"",
                contenido:""
            }
        }
    },
    methods:{
        async crear(){
            await this.axios.post('/api/blog', this.blog)
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