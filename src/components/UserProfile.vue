<template>
    <div class="user-profile">
        <div class="user-profile__user-panel">
            <h1 class="user-profile__username">@{{ user.username }}</h1>
            <div class="user-profile__admin-badge" v-if="user.isAdmin">Admin</div>
            <div class="user-profile__follower-count">
                <strong>Followers: </strong> {{ followers }}
            </div>
        </div>
        <div class="user-profile__twoots-wrapper">
            <TwootItem 
            v-for="twoot in user.twoots" 
            :key="twoot.id" 
            :username="user.username" 
            :twoot="twoot" 
            @favourite="toggleFavourite"
            />
        </div>
    </div>
</template>

<script>
import TwootItem from './TwootItem';

export default {
  name: 'UserProfile',
  components: { TwootItem },

  data(){
    return{
      followers: 0,
      user: {
        id: 1,
        username: 'LoginALee',
        firstName: 'Alejandro',
        lastName: 'Tinoco',
        email: 'admin123@gmail.com',
        isAdmin: true,
        twoots: [
            {
                id: 1,
                content: "Twotter is better than Twitter"
            },
            {
                id: 2,
                content: "Whooosh now youre happy"
            }
        ]
      }
    }
  },

  watch: {
    followers(newFollowerCount, oldFollowerCount){
      if(oldFollowerCount < newFollowerCount){
        console.log(`${this.user.username} has gained a follower!`)
      }
    }
  },

  computed: {
    fullName() {
      return `${this.user.firstName} ${this.user.lastName}`;
    }
    
  },

  methods: {
    followUser(){
      this.followers++;
    },

    toggleFavourite(id){
        console.log(`Favourited Twoot #${id}`)
    }
  },

  mounted(){
    this.followUser();
  }
}
</script>

<style>
.user-profile{
    display: grid;
    grid-template-columns: 1fr 3fr;
    width: 100%;
    padding: 50px 5%;
}

.user-profile__user-panel{
    display: flex;
    flex-direction: column;
    margin-right: 50px;
    padding: 20px;
    background-color: white;
    border-radius: 5px;
    border: 1px solid #DFE3E8;
}

.user-profile__admin-badge{
    background: rebeccapurple;
    color: white;
    border-radius: 5px;
    margin-right: auto;
    padding: 0 10px;
    font-weight: bold;
}

</style>