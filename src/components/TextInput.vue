<template>

  <form class="input-form" v-if="role !== 'Citoyen'" @submit.prevent="submitText">
    <input v-if="role === 'Insider'" type="text" v-model="answer" readonly />
    <input v-else type="text" v-model="text" :disabled="disable"/>
    <button v-if="role === 'Maître'" type="submit" :disabled="disable">Soumettre</button>
  </form>

</template>

<script>
export default {

    // Component Name
    name: 'TextInput',

    props: {
        answer: String,
        role: String
    },

    data() {
        return {
            text: "",
            disable: false
        }
    },

    // Component methods
    methods: {
        submitText() {
            // console.log(this.answer)
            if (this.text) {
                this.$socket.emit("answer", this.text);
                this.disable = true;
            }
        },
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.input-form {
    text-align: center;
}

.input-form input {
    width: 90%;
    box-sizing: border-box;
    margin-bottom: 30px;
    font-size: 30px;
    padding: 20px 0;
    text-align: center;
}

.input-form input:focus {
    outline: 0;
}

.input-form button {
    display: block;
    padding: 10px 30px;
    text-transform: uppercase;
    margin: auto;
}

</style>