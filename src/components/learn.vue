<script setup>
import { ref } from 'vue';


const text = ref('Edit me');
const isCheked = ref(false);
const chickedlist = ref(['tarek']);
const numberSelected = ref();

</script>

<template>
    <h1>
        Welcome To pastion managers : {{ text }}
    </h1>

    <input v-model="text" />

    <h2>
        check box
    </h2>

    <input type="checkbox" v-model="isCheked" />
    <p>{{ isCheked }}</p>

    <h2>
        Multy check box
    </h2>

    <input type="checkbox" id="tarek" value="tarek" v-model="chickedlist" />
    <label for="tarek">tarek</label>
    <input type="checkbox" v-model="chickedlist" value="aya" id="aya" />
    <label for="aya">aya</label>
    <input type="checkbox" v-model="chickedlist" value="anis" id="aya" />
    <label for="anis">anis</label>
    <p>name chicked is : {{ chickedlist }}</p>

    <h3>
        Radio
    </h3>

    <input type="radio" value="1" v-model="numberSelected" />
    <label for="1">1</label>
    <input type="radio" value="2" v-model="numberSelected" />
    <label for="2">2</label>
    <input type="radio" value="3" v-model="numberSelected" />
    <label for="3">3</label>
    <p>number selected is : {{ numberSelected }}</p>

    <select v-model="numberSelected">
        <option value="" disabled>PLEASE SELECT</option>
        <option value="1">1</option>
        <option value="2">2</option>
        <option value="3">3</option>
    </select>

    <h3>
        Multy select
    </h3>

    <select multiple v-model="chickedlist">

        <option value="tarek">tarek</option>
        <option value="aya">aya</option>
        <option value="anis">anis</option>
    </select>
    <p>name chicked is : {{ chickedlist }}</p>


</template>

<style scoped></style>
