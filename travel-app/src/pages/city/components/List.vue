<template>
    <div class="list" ref="wrapper">
        <div>
            <div class="area">
                <div class="title border-topbottom">当前城市</div>
                <div class="button-list">
                    <div class="button-wrapper">
                        <div class="button">{{this.currentCity}}</div>
                    </div>
                </div>
            </div>
            <div class="area">
                <div class="title border-topbottom">热门城市</div>
                <div class="button-list">
                    <div class="button-wrapper" 
                         v-for="item of hot"
                         :key="item.id"
                         @click="handleCityClick(item.name)">
                        <div class="button">{{ item.name }}</div>
                    </div>
                </div>
            </div>
            <div 
                class="area" 
                v-for="(item, key) of cities" 
                :key="key"
                :ref="key"
            >
                <div class="title border-topbottom">{{key}}</div>
                <div class="item-list">
                    <div class="item border-bottom"
                         v-for="innerItem of item"
                         :key="innerItem.id"
                         @click="handleCityClick(innerItem.name)">
                         {{innerItem.name}}
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import Bscroll from 'better-scroll'
import { mapState, mapMutations } from "vuex";
export default {
    name: 'CityList',
    props: {
        hot: Array,
        cities: Object,
        letter: String
    },
    mounted () {
        this.scroll = new Bscroll(this.$refs.wrapper)
    },
    watch: {
        letter () {
            if (this.letter) {
                const element = this.$refs[this.letter][0]
                this.scroll.scrollToElement(element)
            }
        }
    },
    methods: {
        handleCityClick (city) {
        //    this.$store.dispatch('changeCity', city)
        // this.$store.commit('changeCity', city)
        this.changeCity(city)
        this.$router.push('/')
        },
        ...mapMutations(['changeCity'])
    },
    computed: {
        ...mapState({
            currentCity: 'city'
        })
    }
}
</script>

<style lang="stylus" scoped>
    @import '~@/assets/styles/varibles.styl'
    .border-topbottom
        &:before
            border-color: #ccc
        &:after
            border-color: #ccc
    .border-bottom
        &:before
            border-color: #ccc
    .list
        position: absolute 
        top: 4.06rem
        left: 0
        right: 0
        bottom: 0
        overflow: hidden
        .title
            line-height: 1.52rem
            background: #eee
            padding-left: .4rem
            color: #666
            font-size: .70rem
        .button-list
            padding: .2rem 1.2rem .2rem .2rem
            overflow: hidden
            font-size: .70rem
            .button-wrapper
                float: left 
                width: 33.33%
                .button
                    margin: .3rem
                    padding: .3rem 0
                    text-align: center
                    border: .02rem solid #ccc
                    border-radius: .06rem
        .item-list
            font-size: .62rem
            .item
                line-height: 1.48rem
                padding-left: .5rem
</style>


