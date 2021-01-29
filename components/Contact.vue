<template>
    <div class="contact-site">
        <div class="shadow"></div>
        <div class="header">
            <h2>{{ title[lang] }}</h2>
        </div>
        <div class="info">
            <p>{{ info[lang] }}</p>
        </div>
        <form @submit.prevent="sendMessageHandler">
            <label>
                <input 
                    type="text" 
                    v-model="inputs.name" 
                    :placeholder="placeholders[lang].name" 
                    :class="isValid.name ? 'pass' : (isValid.name===false ? 'error' : '')"
                    @change="nameValidator"
                >
            </label>
            <label>
                <input 
                    type="email" 
                    v-model="inputs.email" 
                    :placeholder="placeholders[lang].email" 
                    :class="isValid.email ? 'pass' : (isValid.email===false ? 'error' : '')"
                    @change="emailValidator"
                >
            </label>
            <label>
                <textarea 
                    v-model="inputs.message" 
                    cols="30" 
                    rows="10" 
                    :placeholder="placeholders[lang].message" 
                    :class="isValid.message ? 'pass' : (isValid.message===false ? 'error' : '')"
                    @change="textValidator"
                >
                </textarea>
            </label>
            <button>{{ btnText[lang] }}</button>
        </form>
        <FormErrors 
            v-if="errors.name[lang] || errors.email[lang] || errors.message[lang]" 
            :lang="lang"
            :inputs="inputs" 
            :errors="errors" 
            @close-errors="closeErrors" 
        />
    </div>
</template>

<script>
export default {
    props: ['lang'],
    data: () => ({
        title: { uk: 'Contact', pl: 'Kontakt' },
        info: { 
            uk: 'Please fill out the form to send me a message.', 
            pl: 'Wypełnij formularz, aby wysłać mi wiadomość.' 
        },
        placeholders: {
            uk: { name: 'name', email: 'e-mail', message: 'message' },
            pl: { name: 'nazwa', email: 'e-mail', message: 'wiadomość' }
        },
        btnText: { uk: 'SEND MESSAGE', pl: 'WYŚLIJ WIADOMOŚĆ' },
        inputs: { name: '', email: '', message: '' },
        errors: {},
        isValid: { name: null, email: null, message: null }
    }),
    created() {
        this.errors = this.setErrors();
    },
    methods: {
        setErrors() {
            return { name: {uk:'', pl:''}, email: {uk:'', pl:''}, message: {uk:'', pl:''}};
        },
        closeErrors() {
            this.errors = this.setErrors();
        },
        nameValidator() {
            if(this.inputs.name.length < 3) {
                this.errors.name = {
                    uk: 'Name field should have more than 3 characters',
                    pl: 'Nazwa powinna mieć więcej niż 3 znaki'
                }
            } else {
                this.errors.name = { uk: '', pl: '' };
            }
            this.isValid.name = this.errors.name[this.lang] ? false : true;
        },
        emailValidator() {
            const regexpEmail = /(?:[a-z0-9!#$%&'*+/=?^_`{|}~-]+(?:\.[a-z0-9!#$%&'*+/=?^_`{|}~-]+)*|"(?:[\x01-\x08\x0b\x0c\x0e-\x1f\x21\x23-\x5b\x5d-\x7f]|\\[\x01-\x09\x0b\x0c\x0e-\x7f])*")@(?:(?:[a-z0-9](?:[a-z0-9-]*[a-z0-9])?\.)+[a-z0-9](?:[a-z0-9-]*[a-z0-9])?|\[(?:(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.){3}(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?|[a-z0-9-]*[a-z0-9]:(?:[\x01-\x08\x0b\x0c\x0e-\x1f\x21-\x5a\x53-\x7f]|\\[\x01-\x09\x0b\x0c\x0e-\x7f])+)\])/;
            if(this.inputs.email.length < 3) {
                this.errors.email = {
                    uk: 'Email field should have more than 3 characters',
                    pl: 'Email powinien mieć więcej niż 3 znaki'
                }
            } else if(!this.inputs.email.match(regexpEmail)) {
                this.errors.email = {
                    uk: 'Invalid email adress',
                    pl: 'Nieprawidłowy adres email'
                }
            } else {
                this.errors.email = { uk: '', pl: '' };
            }
            this.isValid.email = this.errors.email[this.lang] ? false : true;
        },
        textValidator() {
            if(this.inputs.message.length < 8) {
                this.errors.message = { 
                    uk: 'Message field should have more than 8 characters',
                    pl: 'Wiadomość powinna mieć więcej niż 8 znaków'
                }
            } else {
                this.errors.message = { uk: '', pl: '' };
            }
            this.isValid.message = this.errors.message[this.lang] ? false : true;
        },
        sendMessageHandler() {
            this.nameValidator();
            this.emailValidator();
            this.textValidator();
            if(this.isValid.name && this.isValid.email && this.isValid.message) {
                alert('message send')
            }
        }
    }
}
</script>