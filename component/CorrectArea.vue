<script setup lang="ts">

const props = defineProps<{
    placeHolder: string,
    isBusy: boolean,
    editable: boolean,
    value: string,
    onChange: (value: string) => void,
    buttonText: string,
    onClick: () => void
}>()

</script>
<template>
    <div class="input-area">
        <textarea :value="value" :disabled="!editable" :placeholder="placeHolder"
            @input="(event: any) => onChange(event.target.value)" rows="10"></textarea>
        <div>
            <button @click="onClick"><span v-if="isBusy" class="loader"></span>{{ buttonText }}</button>
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