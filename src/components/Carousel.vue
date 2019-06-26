<template>
    <div class="roundCarousel stream " :class="{'is-shown': showCarousel}">
        <Slide 
            v-for="(img, i) in images" 
            :key="i" 
            :className="`${classNames[i]} item`"
            :img="img"/>
    </div>
</template>
<script>
import Slide from './Slide.vue'

export default {
    components: {
        Slide
    },
    data() {
        return {
            items: [],
            count: 0,
            classes: [],
            itemcount: 0,
            classNames: [],
            showCarousel: false
        }
    },
    props: {
        images: Array,
        duration: {
            type: Number,
            default: 3000
        }
    },
    methods: {
        getMod(n, m) {
            return ((m % n) + n) % n;
        },
        shiftWatches(transition) {
            this.count = this.getMod(this.itemcount, this.count);

            /* Distribute classes from array */
            for (let i = 0; i < this.itemcount; i++) {
                let clnum = i - this.count;
                clnum = clnum < 0 ? this.itemcount + clnum : clnum;
                const animClass = transition ? ' is-animated' : '';
                const itemClass = this.classes[clnum] ? this.classes[clnum] + animClass : 'is-hidden';
                this.classNames.splice(i, 1)
                this.classNames.splice(i, 0, itemClass);
            } 
        },
        init() {
            this.items = document.querySelectorAll('.roundCarousel .item')
            this.itemcount = this.items.length
            this.classes = ['is-hidden left', 'left-first', 'left-second', 'center', 'right-first', 'right-second', 'is-hidden right']
        }
    },
    mounted() {
        window.onload = () => {

            this.init()

            this.count = Math.floor(Math.random()*this.itemcount);

            this.shiftWatches(false);
            this.showCarousel = true

            window.setInterval(() => {
                this.count--;
                this.shiftWatches(true);
            }, this.duration);

        }
    }
}
</script>
<style lang="css" scoped>

.stream {
  width: 100%;
  height: 32em;
  position: relative;
  margin-bottom: -4em;
  margin-top: 4em;
  overflow: hidden;
  opacity: 0;
  -webkit-transition: 1s opacity;
  transition: 1s opacity; 
}
  .stream.is-shown {
    opacity: 1; 
    }
@media (max-width: 400px) {
    .stream {
      font-size: .9em;
      height: 25em; 
      } 
}

.watch__info {
  position: absolute;
  top: 25em;
  left: 0;
  width: 100%;
  text-align: center;
  opacity: 0;
  pointer-events: none;
  -webkit-transition: .3s opacity;
  transition: .3s opacity;
  -webkit-transition-delay: 0;
          transition-delay: 0;
  display: none; }
  .watch__info__title {
    display: inline-block;
    font-family: "AvenirLTStd-Heavy", Helvetica, Arial, sans-serif;
    font-size: .7em;
    color: #aaa;
    width: 100%;
    line-height: 1.4em;
    text-transform: uppercase;
    padding: 0;
    padding-top: 1.5em;
    margin-bottom: .4em;
    letter-spacing: 1px;
    position: relative; }
    .watch__info__title:before {
      content: "";
      height: 1px;
      width: 40%;
      background-color: #ddd;
      position: absolute;
      top: 0;
      left: 30%;
      display: none; }
  .watch__info__ref {
    font-size: .7em;
    font-family: "AvenirLTStd-Heavy", Helvetica, Arial, sans-serif;
    color: #aaa;
    letter-spacing: 1px;
    line-height: 1.4em; }
  .watch__info__desc {
    line-height: 1.4em;
    font-size: 1.1em;
    display: none; }

.item {
  display: block;
  position: absolute;
  top: 0;
  left: 50%;
  width: 20em;
  margin-left: -10em;
  opacity: 1;
  text-align: center; }
  @media (max-width: 400px) {
    .item {
      font-size: .8em; } }
  .item.is-hidden {
    display: none;
    opacity: 0; }
    .item.is-hidden.left {
      display: block;
      opacity: 0;
      -webkit-transform: scale(0.8) translate3d(-310%, 70%, 0) rotate(-35deg);
              transform: scale(0.8) translate3d(-310%, 70%, 0) rotate(-35deg); }
    .item.is-hidden.right {
      display: block;
      opacity: 0;
      -webkit-transform: scale(0.8) translate3d(310%, 70%, 0) rotate(35deg);
              transform: scale(0.8) translate3d(310%, 70%, 0) rotate(35deg); }
  .item.center {
    z-index: 2; }
    .item.center .watch__info {
      opacity: 1;
      pointer-events: auto;
      -webkit-transition-delay: .4s;
              transition-delay: .4s; }
  .item.left-first {
    z-index: 0;
    -webkit-transform: scale(0.8) translate3d(-225%, 38%, 0) rotate(-28deg);
            transform: scale(0.8) translate3d(-225%, 38%, 0) rotate(-28deg); }
  .item.left-second {
    z-index: 1;
    -webkit-transform: scale(0.8) translate3d(-120%, 10%, 0) rotate(-12deg);
            transform: scale(0.8) translate3d(-120%, 10%, 0) rotate(-12deg); }
  .item.right-first {
    z-index: 1;
    -webkit-transform: scale(0.8) translate3d(120%, 10%, 0) rotate(12deg);
            transform: scale(0.8) translate3d(120%, 10%, 0) rotate(12deg); }
  .item.right-second {
    z-index: 0;
    -webkit-transform: scale(0.8) translate3d(225%, 38%, 0) rotate(28deg);
            transform: scale(0.8) translate3d(225%, 38%, 0) rotate(28deg); }
  .item.is-animated {
    -webkit-transition: 0.4s opacity, 0.7s -webkit-transform cubic-bezier(0.645, 0.045, 0.355, 1);
    transition: 0.4s opacity, 0.7s -webkit-transform cubic-bezier(0.645, 0.045, 0.355, 1);
    transition: 0.7s transform cubic-bezier(0.645, 0.045, 0.355, 1), 0.4s opacity;
    transition: 0.7s transform cubic-bezier(0.645, 0.045, 0.355, 1), 0.4s opacity, 0.7s -webkit-transform cubic-bezier(0.645, 0.045, 0.355, 1); }

.item__image {
  width: 85%;
  -webkit-transform: translateX(10px) translateZ(0);
          transform: translateX(10px) translateZ(0); }
</style>


