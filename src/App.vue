<template>
    <div id="app">
        <img class="logo" src="./assets/logo.png">
        <hello></hello>
        <h1 v-on:click="toggleClass" v-bind:class="{red:isRed,yellow:isYellow}">{{list}}</h1>
        <input type="text" v-model='insertList' @keyup.13='insert'>
        <ul>
            <li v-for="item in items" :class="{blue:item.haveColor}" @click='clearBlue(item)'>{{item.label}}</li>
        </ul>
        <select>
            <option v-for="item in options">
                {{ item.text }}
            </option>
        </select>
        <button v-on:click="broadcastMsg">fatherClick</button>
        <p>{{childwords}}</p>
    </div>
</template>
<script>
import Hello from './components/Hello';
import storage from './storage';

export default {
    components: {
        Hello
    },
    data() {
        return {
            list: "This is a list",
            msg1:'good son',
            childwords: "",
            isRed: false,
            isYellow: true,
            insertList: '',
            items: storage.fetch(),
            options: [{
                text: 'One'
            }, {
                text: 'Two'
            }, {
                text: 'Three'
            }]
        }
    },
    watch: {
        items: {
            handler: function(items) {
                storage.save(items)
            },
            deep: true
        }
    },
    events: {
        'listen-to-son': function(msg) {
            this.childwords = msg
        }
    },
    methods: {
        toggleClass: function() {
            this.$data.isRed = !this.$data.isRed;
            this.$data.isYellow = !this.$data.isYellow;

        },
        clearBlue: function(item) {
            item.haveColor = false;
        },
        insert: function() {
            this.items.push({
                label: this.insertList,
                haveColor: true
            });
            this.insertList = '';

        },
        broadcastMsg:function(){
            this.$broadcast('tomyson',this.msg1);
        }
    }
}
</script>
<style>
html {
    height: 100%;
}

body {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100%;
}

#app {
    color: #2c3e50;
    margin-top: -100px;
    max-width: 600px;
    font-family: Source Sans Pro, Helvetica, sans-serif;
    text-align: center;
}

#app a {
    color: #42b983;
    text-decoration: none;
}

.red {
    color: red;
}

.yellow {
    color: yellow;
}

.blue {
    color: blue;
}

.logo {
    width: 100px;
    height: 100px
}
</style>
