<template>
    <div>
        <h1 class="text-center">Gestionar Articulos</h1>
        <hr>


        <button @click="abrirModal();" type="button" class="btn btn-primary">
         Nuevo
        </button>

        <!-- The Modal -->
        <div class="modal" :class="{mostrar:modal}">
          <div class="modal-dialog">
            <div class="modal-content">

               <!-- Modal Header -->
               <div class="modal-header">
                  <h4 class="modal-title">{{tituloModal}}</h4>
                     <button @click="cerrarModal();" type="button" class="close" data-dismiss="modal">&times;</button>
               </div>

               <!-- Modal body -->
               <div class="modal-body">
                   Modal body..
               </div>

               <!-- Modal footer -->
               <div class="modal-footer">
                   <button @click="cerrarModal();" type="button" class="btn btn-danger" data-dismiss="modal">Cancelar</button>
               </div>

           </div>
          </div>
        </div>


        <table class="table">
               <thead class="thead-dark">
                 <tr>
                   <th scope="col">#</th>
                   <th scope="col">Nombre</th>
                   <th scope="col">Descripcion</th>
                   <th scope="col">Stock</th>
                   <th scope="col" colspan="2" class="text-center">Accion</th>
                 </tr>
               </thead>
                <tbody>
                  <tr v-for="art in articulos" :key="art.id">
                    <th scope="row">{{art.id}}</th>
                    <td>{{art.nombre}}</td>
                    <td>{{art.descripcion}}</td>
                    <td>{{art.stock}}</td>
                    <td>
                        <button class="btn btn-warning">Editar</button>
                    </td>
                    <td>
                        <button @click="eliminar(art.id)" class="btn btn-danger">Eliminar</button>
                    </td>
                  </tr>
                </tbody>
        </table>

    </div>
</template>
<script>
export default {
  data()
  {
      return{
         modal:0,
         tituloModal:'',
         articulos:[],

      }    
  },
  methods: {
       async listar (){
             const res=await axios.get('/articulos');
             this.articulos=res.data;
       },

       async eliminar (id){
           const res= await axios.delete('/articulos/'+id);
           this.listar ();
       },
       abrirModal(){
           this.modal=1;
       },
       cerrarModal(){
           this.modal=0;
       }
  },
  created(){
     this.listar ();
  },

}
</script>

<style>
    .mostrar{
        display: list-item;
        opacity:1;
        background: rgb(44,38,75,0.849);
    }
</style>
