<script>
import { stringifyExpression } from '@vue/compiler-core'
import { toHandlers } from 'vue'

export default {
    props: {
        propFunkcija: function() {
            this.nekaFunkcija()
        }
    },
    data() {
        return {
            images: [
                { url: 'src/logos/image-product-1.jpg', name: 'Fall Limited Edition Sneakers', price: 125.00 },
                { url: 'src/logos/image-product-2.jpg', name: 'Patike', price: 125.00 },
                { url: 'src/logos/image-product-3.jpg', name: 'Tene', price: 125.00 },
                { url: 'src/logos/image-product-4.jpg', name: 'Cizme', price: 125.00 },
            ],
            activePhoto: { url: 'src/logos/image-product-1.jpg', name: 'Fall Limited Edition Sneakers', price: 125.00 },
            counter: 1,
            cart: [],
            price: 0,
            priceTotal: 0,
            imgSrc: '',
            articleName: '',
            articles: '',
            album: false
        }
    },
    methods: {
        counterInc() {
            this.counter++
        },
        counterDec() {
            this.counter--
            if (this.counter <= 0) {
                this.counter = 1
            }
        },
        pushArticle() {
            let images = this.activePhoto
            let shownCart = []
            for (let x in images) {
                this.imgSrc = images.url
                this.price = images.price
                this.priceTotal = images.price * this.counter
                this.articleName = images.name
                shownCart = 
                     {name: this.articleName, counter: this.counter, price: this.price, total: this.priceTotal, img: this.imgSrc }
            }
            /* console.log(shownCart) */
            let products = [];
            products = ("shownCart", shownCart)
            localStorage.setItem("products", JSON.stringify(products));
            let storedProducts = JSON.parse(localStorage.getItem("products"));
            this.articles = storedProducts
            return shownCart;
            // emitaj ga u NAVBAR i napravi if else u cart
        }
    },
}
</script>

<template>
    <div class="album" v-if="album">
        <div class="album-parent">    
            <svg @click="album = false" width="14" height="15" xmlns="http://www.w3.org/2000/svg"><path d="m11.596.782 2.122 2.122L9.12 7.499l4.597 4.597-2.122 2.122L7 9.62l-4.595 4.597-2.122-2.122L4.878 7.5.282 2.904 2.404.782l4.595 4.596L11.596.782Z" fill="#fff" fill-rule="evenodd"/></svg>
            <div class="album-parent__bigImage">
                <img :src="activePhoto.url" alt="Big image">
            </div>
            <div class="album-parent__smalImages" >
                <img :src="image.url" alt="1" v-for="image in images" @click="activePhoto = image" :class="{ 'is-active': image.name === activePhoto.name }">
            </div>
        </div>
    </div>
    <section class="c-section">
        <div class="c-section__left">
            <div class="c-section__left-bigImg">
                <img :src="activePhoto.url" alt="Big image" @click="album = true">
            </div>
            <div class="c-section__left-smallImg" >
                <img :src="image.url" alt="1" v-for="image in images" @click="activePhoto = image" :class="{ 'is-active': image.name === activePhoto.name }">
            </div>
        </div>
        <div class="c-section__right">
            <h2>SNEAKER COMPANY</h2>
            <h1>Fall Limited Edition Sneakers</h1>
            <p>These low-profile sneakers are your perfect casual wear
                companion. Featuring a durable rubber outer sole,
                they'll withstand everything the weather can offer.
            </p>
            <div class="c-section-right-price">
                <h3>$125.00</h3> <div>50%</div>
            </div>
            <p class="old-price">$250.00</p>
            <div class="c-section__right__btns">
                <div class="c-section-btns-counter">
                    <svg @click="counterDec()" width="12" height="4" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"><defs><path d="M11.357 3.332A.641.641 0 0 0 12 2.69V.643A.641.641 0 0 0 11.357 0H.643A.641.641 0 0 0 0 .643v2.046c0 .357.287.643.643.643h10.714Z" id="a"/></defs><use fill="#FF7E1B" fill-rule="nonzero" xlink:href="#a"/></svg>
                    <div>{{counter}}</div>
                    <svg @click="counterInc()" width="12" height="12" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"><defs><path d="M12 7.023V4.977a.641.641 0 0 0-.643-.643h-3.69V.643A.641.641 0 0 0 7.022 0H4.977a.641.641 0 0 0-.643.643v3.69H.643A.641.641 0 0 0 0 4.978v2.046c0 .356.287.643.643.643h3.69v3.691c0 .356.288.643.644.643h2.046a.641.641 0 0 0 .643-.643v-3.69h3.691A.641.641 0 0 0 12 7.022Z" id="b"/></defs><use fill="#FF7E1B" fill-rule="nonzero" xlink:href="#b"/></svg>
                </div>
                <button class="c-section-btns-cart" @click="pushArticle()">
                    <svg width="22" height="20" xmlns="http://www.w3.org/2000/svg"><path d="M20.925 3.641H3.863L3.61.816A.896.896 0 0 0 2.717 0H.897a.896.896 0 1 0 0 1.792h1l1.031 11.483c.073.828.52 1.726 1.291 2.336C2.83 17.385 4.099 20 6.359 20c1.875 0 3.197-1.87 2.554-3.642h4.905c-.642 1.77.677 3.642 2.555 3.642a2.72 2.72 0 0 0 2.717-2.717 2.72 2.72 0 0 0-2.717-2.717H6.365c-.681 0-1.274-.41-1.53-1.009l14.321-.842a.896.896 0 0 0 .817-.677l1.821-7.283a.897.897 0 0 0-.87-1.114ZM6.358 18.208a.926.926 0 0 1 0-1.85.926.926 0 0 1 0 1.85Zm10.015 0a.926.926 0 0 1 0-1.85.926.926 0 0 1 0 1.85Zm2.021-7.243-13.8.81-.57-6.341h15.753l-1.383 5.53Z" fill="#fff" fill-rule="nonzero"/></svg>
                    <div>Add to cart</div>
                </button>
            </div>
        </div>
    </section>
</template>

<style scoped>
.album {
    display: flex;
    flex-direction: column;
    justify-content: center;
    width: 100%;
    max-width: 1268px;
    background-color: rgba(0, 0, 0, 0.4);
    z-index: 100;
    margin: 0 auto;
    position: absolute;
    height: 100vh;
    text-align: center;
    margin-left: auto;
    margin-right: auto;
    left: 0;
    right: 0;
}

.album-parent {
    display: flex;
    flex-direction: column;
    justify-content: center;
    margin: 0 auto;
}
.album-parent svg {
    position: relative;
    display: flex;
    justify-content: flex-end;
    left: 430px;
    top: -20px;
    cursor: pointer;
}
.album-parent__bigImage img{
    display: flex;
    height: 430px;
    width: 100%;
    max-width: 500px;
    border-radius: 15px;
}
.album-parent__smalImages {
    display: flex;
    flex-direction: row;
    width: 450px;
    max-width: 450px;
    justify-content: space-between;
    flex-wrap: wrap;
    margin-top: 30px;
}
.album-parent__smalImages img {
    width: 100%;
    max-width: 90px;
    border-radius: 15px;
    cursor: pointer;
}
.c-section {
    display: flex;
    margin: 0 auto;
    width: 100%;
    max-width: 1268px;
    margin-top: 150px;
    justify-content: space-around;
    flex-wrap: wrap;
    align-items: center;
}
.c-section__left {
    display: flex;
    flex-direction: column;
    height: 570px;
    justify-content: space-between;
}
.c-section__left-bigImg img {
    display: flex;
    height: 430px;
    width: 100%;
    max-width: 500px;
    border-radius: 15px;
    cursor: pointer;
}
.c-section__left-smallImg {
    display: flex;
    flex-direction: row;
    width: 450px;
    max-width: 450px;
    justify-content: space-between;
    flex-wrap: wrap;
}
.c-section__left-smallImg img {
    width: 100%;
    max-width: 90px;
    border-radius: 15px;
    cursor: pointer;
}
.c-section__left-smallImg img:hover {
    opacity: 50%;
}
.c-section__left-smallImg .is-active {
    opacity: 30%;
    border: 3px solid hsl(26, 100%, 55%);
}
.c-section__right {
    display: flex;
    flex-direction: column;
    width: 100%;
    max-width: 400px;
    flex-wrap: wrap;
}
.c-section__right h2 {
    color: orange;
    font-size: 16px;
}
.c-section__right h1 {
    font-size: 40px;
    width: 100%;
    margin: 0;
}
.c-section__right p {
    color: grey;
    font-size: 16px;
    width: 100%;
    line-height: 26px;
}
.c-section-right-price {
    display: flex;
    align-items: center;
}
.c-section-right-price div {
    margin-left: 25px;
    color: orange;
    font-weight: 700;
    background-color: rgb(245, 236, 236);
    border-radius: 6px;
    padding: 2px 5px;
}
.c-section-right-price h3 {
    font-size: 28px;
}
.old-price {
    text-decoration: line-through;
    font-weight: 500;
    margin-top: -20px;
}
.c-section__right__btns {
    display: flex;
    align-items: center;
    flex-wrap: wrap;
    justify-content: space-between;
    margin-top: 25px;
}
.c-section-btns-counter  {
    display: flex;
    align-items: center;
    padding: 15px 25px;
    justify-content: space-between;
    width: 100px;
    border-radius: 8px;
    background-color: rgb(247, 247, 247);
}
.c-section-btns-counter div {
    font-weight: 700;
}
.c-section-btns-counter svg {
    cursor: pointer;
}
.c-section-btns-cart {
    display: flex;
    background-color: hsl(26, 100%, 55%);
    border: none;
    padding: 15px 50px;
    width: 240px;
    justify-content: space-around;
    border-radius: 8px;
    align-items: center;
    cursor: pointer;
}
.c-section-btns-cart div {
    color: white;
    font-weight: 500;
    font-size: 16px;
}

@media (max-width: 500px) {
    .c-section__left {
        margin-bottom: 100px;
    }
}
</style>