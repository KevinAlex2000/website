<template>
    <div class="page-content w-100">
        <div class="cover">
            <img class="background" />
            <div class="display-5">
                {{ proyect.title }}
            </div>
        </div>
        <div class="body px-5">
            <div class="row justify-content-center">
                <div class="col-md-7">
                    <div id="carouselExampleControls" class="carousel slide d-block d-md-none mb-5" data-bs-ride="carousel">
                        <div class="carousel-inner">
                            <div class="carousel-item" v-for="(img, index) in proyect.screenshots" :key="img" :class="{active: index == 0}">
                                <img 
                                    :src="img" 
                                    class="d-block w-100" 
                                    v-on:click="zoomImage(img)" 
                                    data-bs-toggle="modal" 
                                    data-bs-target="#ModalZoomImage">
                            </div>
                        </div>
                        <a class="carousel-control-prev" href="#carouselExampleControls" role="button" data-bs-slide="prev">
                            <span class="carousel-control-prev-icon" aria-hidden="true"></span>
                            <span class="visually-hidden">Previous</span>
                        </a>
                        <a class="carousel-control-next" href="#carouselExampleControls" role="button" data-bs-slide="next">
                            
                            <span class="carousel-control-next-icon" aria-hidden="true"></span>
                            <span class="visually-hidden">Next</span>
                        </a>
                    </div>
                    <div
                        data-bs-toggle="modal" 
                        data-bs-target="#ModalZoomImage"
                        class="mb-3 screenshot d-none d-md-block" 
                        v-for="(img) in proyect.screenshots" 
                        :key="img"
                    >
                        <img :src="img" class="d-block w-100" v-on:click="zoomImage(img)">
                    </div>
                </div>
                
                <div class="col-md-5">
                    <div id="info">
                        <div class="h6 text-uppercase subtitle">
                            Descripción
                        </div>
                        <p class="paragraph">{{ proyect.description_long }}</p>
                        <div class="h6 text-uppercase subtitle">
                            Tecnologías
                        </div>
                        <p class="paragraph">
                            <ul>
                                <li v-for="tecno in proyect.tecnologies" :key="tecno">{{tecno}}</li>
                            </ul>
                        </p>
                        <div  v-if="proyect.github || proyect.link">
                            <div class="h6 text-uppercase subtitle" >
                                Opciones
                            </div>
                            <p class="paragraph">
                                <a target="_blank" v-if="proyect.github" :href="proyect.github">Ver repositorio</a>
                                |
                                <a target="_blank"  v-if="proyect.link" :href="proyect.link">Descargar</a>
                            </p>
                        </div >
                    </div>
                </div>
            </div>
        </div>

        <div class="modal fade" id="ModalZoomImage" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
            <div class="modal-dialog modal-dialog-centered modal-xl">
                <img id="img-zoom" class="w-100" src="">
            </div>
        </div>
    </div>

    
</template>

<script scoped>

export default {
    data() {
        return {
            proyect: {}
        };
    },
    methods: {
        getProyect() {
            this.$axios.get("/data/proyects.json").then((response) => {
                this.proyect = response.data.find(
                    (element) => element.title === this.$route.params.proyect
                );
            });
        },
        moveInfo(){
            const info = document.getElementById("info");

            const topInfo = info.offsetTop -50

            if(window.scrollY > topInfo){
                const difference = window.scrollY - topInfo;
                info.style.cssText = "padding-top: "+difference+"px"
            }else{
                info.style.cssText = "padding-top: 0px"
            }
        },
        zoomImage(url){
            document.getElementById("img-zoom").setAttribute("src",url)
        }
    },
    mounted() {
        this.getProyect();
        window.onscroll = this.moveInfo;
    }
};
</script>

<style lang="scss" scoped>
.page-content {

    .cover {
        position: relative;
        text-align: center;

        padding-top: 100px;
        padding-bottom: 100px;

        @media (min-width:992px) {
            padding-top: 230px;
            padding-bottom: 230px;
        }

        img {
            background-image: url("/img/proyect.jfif");
            background-size: cover;
            object-fit: cover;
            content: "";
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            opacity: 0.5;
            z-index: -1;
        }
    }

    .body {
        padding-top: 90px;
        padding-bottom: 90px;
        margin-left: auto;
        margin-right: auto;
        max-width: 1200px;

        .title,
        .paragraph {
            font-family: "Andika New Basic", sans-serif;
        }

        .paragraph {
            font-size: 16px;
            color: rgb(99, 99, 99);
            margin-bottom: 50px;

            ul{
                padding-left: 0px;
                list-style: none;
                display: flex;

                li{
                    &:after {
                        content: ",";
                        margin-right: 4px;
                    }

                    &:last-child{
                        &:after{
                            content: ".";
                        }
                    }
                }
            }
        }

        .screenshot {
            background-color: black;
        }
        img{
            width: 100%;
            height: 100%;
            opacity: 0.95;
            object-fit: cover;
        }
    }

    .carousel{
        *{
            height: 100%;
        }

        .carousel-control-prev,
        .carousel-control-next{
            &:hover{
                color: var(--color-3);
            }
        }
    }
}
</style>
