<template>
    <div class="conatiner"> 
    <p>{{name}}</p>
    <div class="howMuch"> 
    <p>{{howMuch}} </p>
    </div>
    </div>
</template>

<script>
export default {
    name: 'NavComponent',
    props: {
        name: String,
        howMuch: Number
    }
 }
</script>

<style scoped>
.conatiner {
    display: grid;
    padding: 0.5em;
    grid-template-columns: 90% 10%;
    border-bottom: 1px solid black;
}



p{
    margin: 0 auto;
    margin-left: 0;
}

.howMuch{
    width: 1.2em;
    border-radius: 25px;
    background: #C4C4C4;
    margin: 0 auto;
}

.howMuch > p{
    text-align: center;;
}

</style>