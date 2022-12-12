<script>
export default {
    props: ["onTagsChange"],
    data() {
        return {
            currentValue: "",
            tags: [],//aqui se guardan las etiquetas que se van creando 
        };
    },
    methods: {
        handlekeyDown(e) {//eliminar etiquetas con el backspace
            if (e.key === 'Backspace' && this.currentValue === '') {
                this.tags.pop();
                this.onTagsChange(this.tags);
            }
        },
        handleSubmit() {//guardar nueva etiqueta sin repetir 
            if (this.currentValue !== "") {
                const exist = this.tags.some(item => item === this.currentValue);
                if (!exist) {//si no existe dentro del arreglo se puede agregar
                    this.tags.push(this.currentValue);//agregar el valor a tags 
                    this.currentValue = "";//borrar valor despues de ingresar
                    this.onTagsChange(this.tags);
                }
            }
        },
        delateTag(tag) {//eliminar etiqueta con el boton x 
            this.tags = this.tags.filter((item) => item !== tag);
            this.onTagsChange(this.tags);
        }
    },
};


</script>

<template>
    <h1>Etiquetas</h1>
    <br>
    <div class="imputTag">
        <div class="tags">
            <div class="tag" v-for="(tag, index) in tags" :kay="index">
                {{ tag }} <button @click="delateTag(tag)">X</button>
            </div>

        </div>
        <form @submit.prevent="handleSubmit">
            <input class="imput" type="text" v-model="currentValue" @keydown="handlekeyDown" />
        </form>

    </div>
</template>

<style scoped>
.imputTag {
    display: inline-flex;
    border: solid 1px #000;
    border-radius: 3px;
    height: 50px;
}
h1{
    color:white;
}
.tags {
    display: flex;
    gap: 3px;
    padding: 5px;

}

.tags .tag {
    display: flex;
    padding: 5px;
    border: solid 1px rgb(201, 144, 144);
    gap: 5px;
    align-content: center;
    border-radius: 3px;
}

.imputTag form {
    display: inline-flex;
    
}

.imputTag .imput {
    border: none;
    outline: none;
    padding: 0 5px;
}

.imputTag button {
    background-color: transparent;
    border: none;
    border-radius: 3px;
}

.tag button:hover {
    background-color: #eee;
}
</style>
