<template>
    <div class="hello">
        <h1>{{ msg }}</h1>
        <h2 v-text='msgfromfather1'></h2>
        <button v-on:click="showMsg">sonClick!</button>
        <p>{{msgfromfather}}</p>
    </div>
</template>
<script>
export default {
    data() {
            return {
                msg: "hello word",
                msg1: "good father",
                msgfromfather: '',
            }
        },
        props: ['msgfromfather1'],
        events: {
            'tomyson': function(msg) {
                this.msgfromfather = msg
            }
        },
        methods: {
            showMsg: function() {
                console.log(this.msgfromfather1)
                    // this.$emit("listen-to-son",this.msg1)
                this.$dispatch('listen-to-son', this.msg1)
            }
        },
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1 {
    color: #42b983;
}
</style>
