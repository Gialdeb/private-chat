<template>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-md-3">
                <div class="card card-default">
                    <div class="card-header">
                        Private Chat App
                    </div>

                    <ul class="list-group">
                        <a href="" @click.prevent :key="friend.id" v-for="friend in friends">
                            <li class="list-group-item">{{ friend.name }}</li>
                        </a>
                    </ul>
                </div>
            </div>
            <div class="col-md-9">
                <message-component v-if="open" @close="close"></message-component>
            </div>
        </div>
    </div>
</template>

<script>
    import MessageComponent from './MessageComponent';
    export default {
        data(){
            return {
                open:true,
                friends:[]
            }
        },
        methods:{
          close(){
              this.open = false
          },
            getFriends(){
              axios.post('/getFriends').then(res => this.friends = res.data.data)
              // axios.post('/getFriends').then(res => console.log(res.data));
            }
        },
        created(){
            // this.$on('close', () => this.close())
            this.getFriends()
        },
        components:{MessageComponent},
    }
</script>
