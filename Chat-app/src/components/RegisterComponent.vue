<template>
    <div class="container" style="margin-top: 50px;">
        <div class="row">
            <div class="offset-md-3 col-md-6">
                <form method="POST" v-on:submit.prevent="doRegister">
                    <div class="form-group">
                        <label for="" class="text-white">Enter name</label>
                        <input type="text" class="form-control" name="name">
                    </div>

                    <br>
                    <div class="form-group">
                        <label for="" class="text-white">Enter email</label>
                        <input type="email" class="form-control" name="email">
                    </div>

                    <br>

                    <div class="form-group">
                        <label for="" class="text-white">Enter password</label>
                        <input type="password" class="form-control" name="password">
                    </div>
                    <br>

                    <input type="submit" class="btn btn-primary" 
                    v-bind:value="isLoading ? 'Loading...' : 'Register'" 
                    v-bind:disabled="isLoading"  name="submit">
                </form>
            </div>
        </div>
    </div>
</template>

<script>
import axios from "axios"
import swal from "sweetalert2"
export default {
    data() {
        return {
            "isLoading": false
        }
    },

    methods: {
        doRegister: async function () {
            const form = event.target;
            const formData = new FormData(form);

            this.isLoading = true;

            const response = await axios.post(
                this.$apiURL + "/registration",
                formData
            );

            this.isLoading = false;
            swal.fire("Success", response.data.message, "success");

            if (response.data.status == "success") {
                form.reset();
            }
        }
    }
}
</script>
