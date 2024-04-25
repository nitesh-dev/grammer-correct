<script setup lang="ts">
const props = defineProps<{
    placeHolder: string,
    isBusy: boolean,
    editable: boolean,
    value: string,
    onChange: (value: string) => void,
    buttonText: string,
    onClick: () => void,
    onLanguageChange: (value: string) => void
}>()


const languages = ['English', 'Hindi']


</script>
<template>
    <div class="input-area">
        <textarea :value="value" :disabled="!editable" :placeholder="placeHolder"
            @input="(event: any) => onChange(event.target.value)" rows="10"></textarea>
        <div>
            <select v-if="editable" @input="(event: any) => onLanguageChange(event.target.value)">
                <option v-for="item, index in languages" :key="index">{{ item }}</option>
            </select>
            <button @click="onClick">
                <span v-if="isBusy" class="loader"></span> {{ buttonText }}
            </button>
        </div>
    </div>
</template>
<style scoped>
.input-area {
    border: 1px solid rgb(223, 223, 223);
}

.input-area div {
    background-color: whitesmoke;
    /* height: 3rem; */
    padding: 0.5rem 1rem;
    display: flex;
    justify-content: flex-end;
    gap: 1rem;
}


.input-area select {
    background-color: white;
    color: rgb(51, 51, 51);
    border: none;
    padding: 0.5rem 1rem;
    border-radius: 4px;
    cursor: pointer;
    transition: all 200ms;
    border: 1px solid rgb(223, 223, 223);
    outline: none;
}



.input-area textarea {
    width: 100%;
    border-radius: 5px;
    padding: 1em;
    font-size: 16px;
    resize: none;
    border: none;
    outline: none;
}

button {
    background-color: var(--color-primary);
    color: white;
    border: none;
    padding: 0.5rem 1rem;
    border-radius: 4px;
    cursor: pointer;
    transition: all 200ms;
    display: flex;
    align-items: center;
    gap: 0.5rem;

}


button:hover {
    opacity: 0.8;
}
</style>