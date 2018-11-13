<template>
  <div class="Main">
      <div class="article" v-for="(tshirt, i) in nvtbl" :key="i" >
          <h3>{{tshirt.name}}</h3> 
          <figure>
              <img :src="tshirt.img"  alt="">
              <h4>{{tshirt.price}}€</h4>
          </figure>
      </div>

  </div>
</template>

<script>
export default {
  name: 'Main',
  data() {
        return {
            range:"",
            brands:[],
            couleurs:"",
            colors:[],
            nvtbl:[],
            colect: [{ name: "adidas Blanc pour Femme", brand: "adidas", img: require("@/assets/img/adidasFBlanc.jpg"), color:"Blanc", price:"10"},
                { name: "adidas Bleu pour Femme", brand: "adidas", img: require("@/assets/img/adidasFBleu.jpg"), color:"Bleu", price:"15"},
                { name: "adidas Noir pour Femme", brand: "adidas", img: require("@/assets/img/adidasFNoir.jpg"), color:"Noir", price:"20"},
                { name: "filas Noir pour Homme", brand: "filas", img: require("@/assets/img/filasHNoir.jpg"), color:"Noir", price:"25"},
                { name: "filas Orange pour Homme", brand: "filas", img: require("@/assets/img/filasHOrange.jpg"), color:"Orange", price:"30"},
                { name: "filas Vert pour Homme", brand: "filas", img: require("@/assets/img/filasHVert.jpg"), color:"Vert", price:"35"},
                { name: "nike Blanc pour Homme", brand: "nike", img: require("@/assets/img/nikeHBlanc.jpg"), color:"Blanc", price:"40"},
                { name: "nike Noir pour Homme", brand: "nike", img: require("@/assets/img/nikeHNoir.jpg"), color:"Noir", price:"45"},
                { name: "nike Rouge pour Homme", brand: "nike", img: require("@/assets/img/nikeHRouge.jpg"), color:"Rouge", price:"50"},
                { name: "puma Orange pour Femme", brand: "puma", img: require("@/assets/img/pumaFOrange.jpg"), color:"Orange", price:"55"},
                { name: "puma Rouge pour Femme", brand: "puma", img: require("@/assets/img/pumaFRouge.jpg"), color:"Rouge", price:"60"},
                { name: "puma Vert pour Femme", brand: "puma", img: require("@/assets/img/pumaFVert.jpg"), color:"Vert", price:"65"}]
        }
    },
  created() {
        this.nvtbl=this.colect;
        console.log(this.nvtbl);
        
        
        this.$ebus.$on("valeur-range", (payload) => {
            this.range=payload;
            this.nwtbl();
        });
        this.$ebus.$on("valeur-brands", (payload) => {
            this.brands=payload;
            this.nwtbl();
        });
        this.$ebus.$on("valeur-couleurs", (payload) => {
            this.colors=payload;
            this.nwtbl();
        });
        console.log(this.range + "range");
        console.log(this.brands + "brands");
        console.log(this.couleurs + "couleurs");
    },
    methods: {
        action(evt) {
            this.msgActuel = evt.msg;
            this.$ebus.$emit("hello-je-pars-en-bus", {done:true})
        },

        nwtbl(){
            this.nvtbl =[];
            this.colect.forEach(i => {
                if(i.price <= this.range ){
                    this.nvtbl.push(i);
                }  
                else {
                    if(this.nvtbl.length==0){
                        this.nvtbl=this.colect;
                        
                    }
                    
                }              
            }); 
            this.nvtbl=this.forBrands(this.nvtbl);
            this.nvtbl=this.forColor(this.nvtbl);
        },

        forBrands(tbl){
            var tblProp=tbl;
            var bl=[];                 
            this.brands.forEach(element => {
                var compte=0;
                tbl.forEach(indice => {
                    if(element == indice.brand){
                        bl.push(indice);
                        console.log("jsuis dans le premier if la ooooooy"+element);
                        
                    }
                    if(element != indice.brand){                        
                        compte ++;                        
                        if (compte == tbl.length && this.brands.length>=1) {
                            console.log("on ets dans le tableau brands");
                            tbl=[];
                        }
                        if (this.brands.length>=4) {
                            console.log("on met le tableau a neuf");
                            tbl=tblProp;
                        }
                    }
                });
            });
            if (bl.length) {
                return bl;
            }else{
                return tbl;
            }
        },

        forColor(tbl){
            var tblProp=tbl;
            var bl=[];                 
            this.colors.forEach(element => {
                var compte=0;
                tbl.forEach(indice => {
                    if(element == indice.color){
                        bl.push(indice);
                    }
                    if(element != indice.color){
                        compte ++;
                        if (compte == tbl.length && this.colors.length>=1) {
                            console.log("on ets dans le tableau colors");
                            tbl=[];
                        }
                        if (this.colors.length>=6) {
                            console.log("on met le tableau a neuf 9 quoi lol  colors");
                            tbl=tblProp;
                        }
                    }
                });
            });
            if (bl.length) {
                return bl;
            }else{
                return tbl;
            }
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
* {
	margin: 0;
	padding: 0;
	border: 0;
	font-size: 100%;
	font: inherit;
	vertical-align: baseline;
}

.Main {    
    max-width: 70vw;
    height: 500px;
    position: relative;
    padding-left: 200px;
    overflow: auto;
    display: flex;
    flex-flow: row wrap;    
}
.article {
    width: 30%;
    height: 300px;
    margin: 10px 5px; 
    float: left;
    border: 1px solid rgba(151, 148, 148, 0.5);    
    background: rgba(174, 171, 171, 0.5);
}
h3 {
    height: 10%;
    width: 100%;
    font-size: 12px;
    float: left
}
figure {
    height: 90%;
    width: 100%;
    float: left
}

img {
    width: 100%;
    height: 80%;
    padding: 15px 0px;
    float: left;
}
h4 {
    height: 10%;
    width: 100%;
    float: left;
    text-align: end;
}
</style>
