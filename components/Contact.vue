<template>
    <div class="contact-site">
        <div class="shadow"></div>
        <div class="header">
            <h2>Contact</h2>
        </div>
        <div class="info">
            <p>Please fill out the form to send me a message.</p>
        </div>
        <form @submit.prevent="sendMessageHandler">
            <label>
                <input 
                    type="text" 
                    v-model="inputs.name" 
                    placeholder="name" 
                    :class="isValid.name ? 'pass' : (isValid.name===false ? 'error' : '')"
                    @change="nameValidator"
                >
            </label>
            <label>
                <input 
                    type="email" 
                    v-model="inputs.email" 
                    placeholder="e-mail" 
                    :class="isValid.email ? 'pass' : (isValid.email===false ? 'error' : '')"
                    @change="emailValidator"
                >
            </label>
            <label>
                <textarea 
                    v-model="inputs.message" 
                    cols="30" 
                    rows="10" 
                    placeholder="message" 
                    :class="isValid.message ? 'pass' : (isValid.message===false ? 'error' : '')"
                    @change="textValidator"
                >
                </textarea>
            </label>
            <button>send message</button>
        </form>
        <FormErrors 
            v-if="errors.name || errors.email || errors.message" 
            :inputs="inputs" 
            :errors="errors" 
            @close-errors="closeErrors" 
        />
    </div>
</template>

<script>
export default {
    data() {
        return {
            inputs: {
                name: '',
                email: '',
                message: ''
            },
            errors: {
                name: '',
                email: '',
                message: ''
            },
            isValid: {
                name: null,
                email: null,
                message: null
            }
        }
    },
    methods: {
        closeErrors() {
            this.errors = {
                name: '',
                email: '',
                message: ''
            }
        },
        nameValidator() {
            if(this.inputs.name.length < 3) {
                this.errors.name = 'Name field should have more than 3 characters';
            } else {
                this.errors.name = '';
            }
            this.isValid.name = this.errors.name ? false : true;
        },
        emailValidator() {
            const regexpEmail = /(?:[a-z0-9!#$%&'*+/=?^_`{|}~-]+(?:\.[a-z0-9!#$%&'*+/=?^_`{|}~-]+)*|"(?:[\x01-\x08\x0b\x0c\x0e-\x1f\x21\x23-\x5b\x5d-\x7f]|\\[\x01-\x09\x0b\x0c\x0e-\x7f])*")@(?:(?:[a-z0-9](?:[a-z0-9-]*[a-z0-9])?\.)+[a-z0-9](?:[a-z0-9-]*[a-z0-9])?|\[(?:(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.){3}(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?|[a-z0-9-]*[a-z0-9]:(?:[\x01-\x08\x0b\x0c\x0e-\x1f\x21-\x5a\x53-\x7f]|\\[\x01-\x09\x0b\x0c\x0e-\x7f])+)\])/;
            if(this.inputs.email.length < 3) {
                this.errors.email = 'Email field should have more than 3 characters';
            } else if(!this.inputs.email.match(regexpEmail)) {
                this.errors.email = 'Invalid email adress';
            } else {
                this.errors.email = '';
            }
            this.isValid.email = this.errors.email ? false : true;
        },
        textValidator() {
            if(this.inputs.message.length < 8) {
                this.errors.message = 'Message field should have more than 8 characters';
            } else {
                this.errors.message = '';
            }
            this.isValid.message = this.errors.message ? false : true;
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