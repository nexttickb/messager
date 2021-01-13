<template>
<div class="bottom">
	<div @click="showPage('Messages')" :class="['item', nowSelect=='Messages'?'active':'default']">
		<div class="icon chat"></div>
		<div class="text">Messages</div>
	</div>
	<div  @click="showPage('Contacts')" :class="['item', nowSelect=='Contacts'?'active':'default']">
		<div class="icon contact"></div>
		<div class="text">Contacts</div>
	</div>
	<div @click="showPage('Settings')" :class="['item', nowSelect=='Settings'?'active':'default']">
		<div class="icon user"></div>
		<div class="text">My</div>
	</div>
</div>
</template>

<script>
export default {
    name: 'Bottom',
    props: {
    },
    components:{},
    data() {
        return {
			nowSelect:''
        }
    },
    computed: {
		
    },
	mounted:function(){
		var self = this;
		RUNKIT.VoimBus.subscribe('public', (topic, res)=>{
			if('showPage' == res.type){
				console.log('showPage:', res.data, this);
				this.nowSelect = res.data.name + '';
			}
		});
		
	},
    methods: {
		showPage(name, param){
            RUNKIT.APP.showPage(name, param || {}, this.$options.name); 
        }
    }
}
</script>

<style lang='less'>

	.bottom{
		height:3.3rem;
		background:#fff;
		display:flex;
		text-align:center;
		box-sizing:border-box;
		box-shadow: 0px 1px 10px #ccc;
		color:#888;
		.item{
			flex:1;
			.icon{
				height:2rem;
			}
			.text{
				height:1.3rem;line-height:0.9rem;font-size:1rem;
			}
			&:active{
				color:#000;
			}
		}
	}
	.default{
		filter: grayscale(100%);
		opacity:0.6;
	}
	.active{
		color:#000;
	}
	.chat{
		background:url('../assets/icon/chat.svg') no-repeat center center;
		background-size:79% 79%;
	}
	.contact{
		background:url('../assets/icon/contacts.svg') no-repeat center center;
		background-size:79% 79%;
	}
	.user{
		background:url('../assets/icon/user.svg') no-repeat center center;
		background-size:79% 79%;
	}
	
</style>
