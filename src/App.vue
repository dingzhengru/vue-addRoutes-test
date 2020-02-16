<template>
<div id="app">
    <div id="nav">
        <router-link to="/">Home</router-link> |
        <router-link to="/about">About</router-link>
    </div>
    <p v-for="(route, index) in routes"
         :key="index">
        <router-link :to="route.path">{{ route.name }}</router-link>
    </p>
    <p>
        <button @click="addRoutes()">addRoutes</button>
    </p>
    <router-view/>
</div>
</template>

<script>
import User from './views/User.vue'
export default {
    name: 'App',
    data() {
        return {

        }
    },
    computed: {
        routes() {
            return this.$router.options.routes
        }
    },
    mounted() {
        // console.log('this.$router', this.$router)
        console.log('this.$router.options.routes', this.$router.options.routes)
    },
    methods: {
        addRoutes() {
            let userRoute = {
                path: '/user',
                name: 'User',
                component: User
            }
            this.$router.options.routes.push(userRoute)


            this.$router.addRoutes(
                [
                    {
                        path: '/user',
                        name: 'User',
                        component: User,
                        meta: { 
                            roles: ['admin', 'editor'] 
                        }
                    }
                ]
            )
            console.log(this.$router.options.routes)

            // 強制更新
            this.$forceUpdate()
        }
    }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
