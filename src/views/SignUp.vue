vue
<template>
    <form @submit.prevent="handleSubmit">
        <h3>Sign Up</h3>
        <div class="form-group">
            <label>First Name</label>
            <input type="text" class="form-control" v-model="firstName" placeholder="First Name" required />
        </div>
        <div class="form-group">
            <label>Last Name</label>
            <input type="text" class="form-control" v-model="lastName" placeholder="Last Name" required />
        </div>
        <div class="form-group">
            <label>Email</label>
            <input type="email" class="form-control" v-model="email" placeholder="Email" required />
        </div>
        <div class="form-group">
            <label>Password</label>
            <input type="password" class="form-control" v-model="password" placeholder="Password" required />
        </div>
        <div class="form-group">
            <label>Confirm Password</label>
            <input type="password" class="form-control" v-model="confirmPassword" placeholder="Confirm Password" required />
            <p v-if="passwordMismatch" style="color: red;">Passwords do not match.</p>
        </div>
        <button type="submit" :disabled="passwordMismatch" class="btn-submit" style="background-color: darkgreen;">Submit</button>
    </form>
</template>

<script>

export default {
    // eslint-disable-next-line vue/multi-word-component-names
    name: 'Signup',
    data() {
        return {
            firstName: '',
            lastName: '',
            email: '',
            password: '',
            confirmPassword: ''
        };
    },
    computed: {
        passwordMismatch() {
            return this.password !== this.confirmPassword;
        }
    },
    methods: {
        handleSubmit() {
            if (this.passwordMismatch) {
                alert("Passwords do not match.");
                return;
            }
            // Handle the signup logic here (e.g., API call)
            console.log('Form submitted:', {
                firstName: this.firstName,
                lastName: this.lastName,
                email: this.email,
                password: this.password
            });

            
        },
        resetForm() {
            this.firstName = '';
            this.lastName = '';
            this.email = '';
            this.password = '';
            this.confirmPassword = '';
        }
    }
};
</script>

<style scoped>
.signup-container {
    max-width: 400px;
    margin: 0 auto;
    padding: 20px;
    border: 1px solid #e0e0e0;
    border-radius: 8px;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
    background-color: #fff;
}
.signup-form {
    display: flex;
    flex-direction: column;
}
h3 {
    text-align: center;
    margin-bottom: 20px;
    color: #333;
}
.form-group {
    margin-bottom: 15px;
}
label {
    margin-bottom: 5px;
    font-weight: bold;
    color: #555;
}
.form-control {
    width: 100%;
    padding: 12px;
    border: 1px solid #ccc;
    border-radius: 4px;
    transition: border-color 0.3s;
}
.form-control:focus {
    border-color: #2874a7;
    outline: none;
    box-shadow: 0 0 5px rgba(40, 167, 69, 0.5);
}
.btn-submit {
    background-color: hsl(199, 86%, 45%);
    color: white;
    padding: 12px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    font-size: 16px;
    transition: background-color 0.3s;
}
.btn-submit:hover:not(:disabled) {
    background-color: #218838;
}
.btn-submit:disabled {
    background-color: #272ad8;
    cursor: not-allowed;
}
.error-message {
    color: red;
    font-size: 0.9em;
    margin-top: 5px;
}
</style>