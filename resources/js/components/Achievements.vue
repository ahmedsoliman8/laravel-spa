<template>
    <div>
        <h1 class="font-normal text-3xl text-grey-darkest leading-none mb-8">
            Your  Achievements
        </h1>
        <p class="text-red italic text-sm"  v-if="message" v-text="message"></p>
      <input type="text" v-model="token" @keyup.enter="fetchAchievements" placeholder="LaracastsApiToken" class="border p-2 rounded w-full mb-8"/>
        <ul>
            <li v-if="achievements.length>0"  v-for="achievement in achievements" v-text="achievement.name"></li>
        </ul>

    </div>
</template>

<script>
export default {

    data(){
        return{
            achievements:[],
            token:'',
            message:''
        }
    },
    methods:{
        fetchAchievements() {
            axios.get(`http://127.0.0.1:8000/api/achievements?api_token=${this.token}`)
                .catch(error=>{
                   // console.log(error.response.data.message);
                    this.message=error.response.data.message;
                    this.achievements=[];
                })
                .then(({data})=>{
                    this.achievements=data;
                    this.message=null;
                });
        }
    }


}
</script>
