<template>
    <div class="wrapper" ref="wrapper">
      <div class="content">
        <slot></slot>
      </div>
    </div>
</template>

<script>
  import BScroll from 'better-scroll'

    export default {
        name: "Scroll",
          data(){
            return {
              scroll:null
            }
        },
        props:{
          probeType:{
            Array:Number,
            default:0
          },
          pullUpLoad:{
            Array: Boolean,
            default: false
          }
        },
        mounted() {
          //创建BScroll对象
          this.scroll = new BScroll(this.$refs.wrapper,{
            click:true,
            probeType: this.probeType,
            pullUpLoad:this.pullUpLoad
          })
          //监听滚动的位置
          this.scroll.on('scroll',(position)=>{
            // console.log(position);
            this.$emit('scroll',position)
          })
          //监听上拉事件
          this.scroll.on('pullingUp',()=>{
            // console.log('上拉加载更多');
                this.$emit('pullingUp')
          })
        },
        methods:{
          scrollTo(x,y,time){
             this.scroll && this.scroll.scrollTo(x,y,time)
          },
          finishPullUp(){
            this.scroll.finishPullUp();
          },
          refresh(){
            this.scroll && this.scroll.refresh();
          },
          getScrollY(){
            return this.scroll.y ? this.scroll.y : 0
          }
        }

    }
</script>

<style scoped>

</style>
