<template>
        <div class="card card-default chat-box">
            <div class="card-header">
                <strong :class="{'text-danger':session_block}">
                    User Name
                    <span v-if="session_block">(Bloccato)</span>
                </strong>

                <!-- Chiusura della chat -->
                <a href="" @click.prevent="close">
                    <i class="fa fa-times float-right" aria-hidden="true"></i>
                </a>
                <!-- / Chiusura della chat -->

                <!-- Opzioni-->
                <div class="dropdown float-right mr-4">
                    <a href="" data-toggle="dropdown" class="dropdown-toggle"  aria-haspopup="true" aria-expanded="false">
                        <i class="fa fa-ellipsis-v" aria-hidden="true"></i>
                    </a>
                    <div class="dropdown-menu" aria-labelledby="dropdownMenuButton">
                        <a href="#" class="dropdown-item" v-if="session_block" @click.prevent="unblock">Sblocca</a>
                        <a href="#" class="dropdown-item" v-else @click.prevent="block">Blocca</a>

                        <a href="#" class="dropdown-item" @click.prevent="clear">Clear Chat</a>
                    </div>
                </div>
                <!-- / Opzioni -->

            </div>
            <div class="card-body" v-chat-scroll>
                <p class="card-text" v-for="chat in chats" :key="chat.message">
                    {{chat.message}}
                </p>
            </div>
            <form class="card-footer" @submit.prevent="send">
                <div class="form-group">
                    <input type="text" class="form-control" placeholder="Scrivi qua il tuo messaggio..." :disabled="session_block">
                </div>

            </form>
        </div>
</template>

<script>
    export default {
        name: "MessageComponent",
        data(){
          return{
              chats:[],
              session_block: false
          }
        },
        created(){
            this.chats.push(
                    {message: 'Ciao'},
                    {message: 'come stai?'},
                    {message: 'bene grazie'},
                )
        },
        methods:{
            send(){
                console.log('yeahhhh');
            },
            close(){
                this.$emit('close')
            },
            clear(){
                this.chats = []
            },
            block(){
                this.session_block = true
            },
            unblock(){
                this.session_block = false
            }
        }
    }
</script>

<style scoped>

    .chat-box{
        height: 400px;
    }

    .card-body{
        overflow-y: scroll;
    }

</style>