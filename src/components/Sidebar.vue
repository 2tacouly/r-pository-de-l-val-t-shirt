<template>
  <div class="Sidebar">
    <button>reset filter</button>
    <hr>
    <h2>Price max</h2>
    <input type="range" min="10" max="65" v-model="range" @change="rangee" >
    {{range}}€ variable valeur range
    <hr>
    <h2>Brands</h2>

    <fieldset>

        <div>
            <input type="checkbox" id="nike" v-model="brands"
                value="nike" @change="brandss" />
            <label for="nike">Nike</label>
        </div>

        <div>
            <input type="checkbox" id="adidas" v-model="brands"
                value="adidas" @change="brandss" />
            <label for="adidas">Adidas</label>
        </div>

        <div>
            <input type="checkbox" id="filas" v-model="brands"
                value="filas" @change="brandss" />
            <label for="filas">Filas</label>
        </div>

        <div>
            <input type="checkbox" id="puma" v-model="brands"
                value="puma" @change="brandss" />
            <label for="puma">Puma</label>
        </div>
        voici les marque selectionner : {{brands}}

    </fieldset>
    <hr>
    <h2>Colors</h2>
    <fieldset id=color>
        <label><input type="checkbox" class="color rouge" value="Rouge" v-model="couleurs" @change="colors" ><span></span></label>
        <label><input type="checkbox" class="color noir" value="Noir" v-model="couleurs" @change="colors" ><span></span></label>
        <label><input type="checkbox" class="color bleu" value="Bleu" v-model="couleurs" @change="colors" ><span></span></label>
        <label><input type="checkbox" class="color blanc" value="Blanc" v-model="couleurs" @change="colors" ><span></span></label>
        <label><input type="checkbox" class="color orange" value="Orange" v-model="couleurs" @change="colors" ><span></span></label>
        <label><input type="checkbox" class="color vert" value="Vert" v-model="couleurs" @change="colors" ><span></span></label>
        {{couleurs}}
    </fieldset>
  </div>
</template>

<script>
export default {
  name: 'Sidebar',
  data(){
        return { 
            range:"",
            brands:[],
            couleurs:[],
        };
    },
    components: {
  },
    methods: {
        rangee(){
          this.$ebus.$emit('valeur-range', this.range)
        },
        brandss() {
            this.$ebus.$emit('valeur-brands', this.brands)
        },
        colors() {
            this.$ebus.$emit('valeur-couleurs', this.couleurs)
        }
    }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

.Sidebar {
    z-index: 3;
    width: 200px;
    height: auto;
    position: fixed;
    float: left;
}
fieldset {
    text-align: left;
    border: none;
}
fieldset#color input{
    appearance: none;
}
#color {
    width: 100%;
    float: left;
    height: 60px;
}
.color {
    width: 20px;
    height: 20px;
    margin: 5px;
    border: 1px solid black;
    float: left;
}

.rouge {
    background: red;
}
.blanc {
    background: white; 
}
.noir {
    background: black;
}
.bleu {
    background: blue;
}
.vert {
    background: green;
}
.orange {
    background: orange;
}
</style>
