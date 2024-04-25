<script setup lang="ts">
import CorrectArea from '~/component/CorrectArea.vue';
import TranslateArea from '~/component/TranslateArea.vue';


const grammarData = ref<string>('')
const aiGrammarData = ref<string>('')
const isGrammarBusy = ref<boolean>(false)
const isTranslateBusy = ref<boolean>(false)





function onGrammarChange(value: string) {
    console.log(value)
    grammarData.value = value
}

async function onGrammarSubmit() {
    if (isGrammarBusy.value) return

    isGrammarBusy.value = true
    const options = {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json'
        },
        body: JSON.stringify({ content: grammarData.value })
    };
    try {
        const response = await fetch("https://chatgpt-clg-backend.onrender.com/api/grammer-correct", options);
        const data = await response.json() as { response: string }
        aiGrammarData.value = data.response

    } catch (error) {
        console.error('Error:', error);

    }

    isGrammarBusy.value = false

}

function copyGrammar() {
    copyToClipboard(aiGrammarData.value)
    alert('copied')
}


function copyToClipboard(text: string) {
    navigator.clipboard.writeText(text);
}




const selectedLanguage = ref<string>('English')
const aiTranslateData = ref<string>('')
const translateData = ref<string>('')

function onLanguageChange(value: string) {
    selectedLanguage.value = value
    console.log(value)
}


function copyTranslate() {
    copyToClipboard(aiTranslateData.value)
    alert('copied')
}

function onTranslateChange(value: string) {
    console.log(value)
    translateData.value = value
}



async function onTranslateSubmit() {
    if (isTranslateBusy.value) return
    isTranslateBusy.value = true
    const options = {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json'
        },
        body: JSON.stringify({ content: translateData.value, language: selectedLanguage.value })
    };
    try {
        const response = await fetch("https://chatgpt-clg-backend.onrender.com/api/translate", options);
        const data = await response.json() as { response: string }
        aiTranslateData.value = data.response

    } catch (error) {
        console.error('Error:', error);

    }

    isTranslateBusy.value = false
}

</script>
<template>
    <div class="section">
        <h1 class="center">Transform your grammatically error with the help of AI</h1>
        <div class="transform-area">
            <div>
                <CorrectArea :onClick="onGrammarSubmit" button-text="Submit" place-holder="Write something..."
                    :editable="true" :onChange="onGrammarChange" :isBusy="isGrammarBusy" :value="grammarData" />
            </div>
            <div>
                <CorrectArea :onClick="copyGrammar" button-text="Copy" place-holder="" :editable="false"
                    :onChange="() => { }" :is-busy="false" :value="aiGrammarData" />
            </div>
        </div>

        <br>
        <br>
        <br>
        <h1 class="center">Translate your language easily with the help of AI</h1>
        <div class="transform-area">
            <div>
                <TranslateArea :onClick="onTranslateSubmit" button-text="Translate" place-holder="Write something..."
                    :editable="true" :onChange="onTranslateChange" :isBusy="isTranslateBusy" :value="translateData"
                    :onLanguageChange="onLanguageChange" />
            </div>
            <div>
                <TranslateArea :onClick="copyTranslate" button-text="Copy" place-holder="" :editable="false"
                    :onChange="() => { }" :is-busy="false" :value="aiTranslateData"
                    :onLanguageChange="onLanguageChange" />
            </div>
        </div>

    </div>
</template>


<style scoped>
.section {
    max-width: 1280px;
    margin: 0 auto;
    margin-top: 3rem;
    margin-bottom: 3rem;
}

.section>* {
    margin-left: 1rem;
    margin-right: 1rem;
}


.transform-area {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 1rem;
}


.center {
    text-align: center;
}


@media only screen and (max-width: 800px) {

    .transform-area {
        grid-template-columns: 100%;
    }
}
</style>


<style>
body {
    margin: 0;
}


:root {
    --color-primary: #0496ff;
    --color-surface: #00a7fb11;
}

h1,
h2,
h3 {
    color: rgb(87, 87, 87);
}

* {
    box-sizing: border-box;
    font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
}



/* loader */

.loader {
    display: block;
    border: 2px solid rgb(255, 255, 255);
    border-left-color: transparent;
    border-radius: 50%;
}

.loader {
    border: 2px solid rgb(255, 255, 255);
    border-left-color: transparent;
    width: 16px;
    height: 16px;
}

.loader {
    border: 2px solid rgb(255, 255, 255);
    border-left-color: transparent;
    width: 16px;
    height: 16px;
    animation: spin89345 1s linear infinite;
}

@keyframes spin89345 {
    0% {
        transform: rotate(0deg);
    }

    100% {
        transform: rotate(360deg);
    }
}
</style>