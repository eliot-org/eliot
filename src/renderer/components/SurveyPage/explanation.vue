<template>
    <div class="explanationWrapper">
        <div class="explanationText" v-html="content.text"></div>
        <button @click="nextPage()" type="button" class="btn-black" v-if="delayOver">
            <span class="btn-text">Next</span>
        </button>
    </div>
</template>

<script>
    export default {
        props:{
            //The Content to show
            content:{               
               required: true
            }
        },
		data: function(){	
			return{
                //Show Continue Button delay, has it expired?
                delayOver: false
			}
		},
		methods:{
            showContinueButton: function(){
                this.delayOver = true
            },
            nextPage: function(){
                this.$emit("nextPage")
            },
            //Init data
            init(){
                if(Object.prototype.hasOwnProperty.call(this.content, "continueDelay")){
                    if(this.content.continueDelay != "-1" && this.content.continueDelay != -1){
                        setTimeout(() => {this.delayOver = true}, this.content.continueDelay * 1000)
                    }
                }else{
                    this.delayOver = true
                }
            },
        },
        mounted(){
            //Init after small timeout so that all data is really loaded
            setTimeout(()=>{this.init()},10)
        },
    }
</script>

<style scoped>   
</style>