<script setup>
    import { ref } from 'vue';
    import { Notyf } from 'notyf';
    import 'notyf/notyf.min.css';

    const notyf = new Notyf();

    const WEB3FORMS_ACCESS_KEY = "bdd05f4f-ae00-4f98-b18c-1289f539c384";

    const subject = "New Message from Portfolio Contact Form";

    const name = ref('');
    const email = ref('');
    const message = ref('');

    const isLoading = ref(false);

    const submitForm = async () => {
        isLoading.value = true;

        try{
            const response = await fetch("https://api.web3forms.com/submit", {
                method: "POST",
                headers: {
                    "Content-Type": "application/json",
                    Accept: "application/json"
                },
                body: JSON.stringify({
                    access_key: WEB3FORMS_ACCESS_KEY,
                    subject: subject,
                    name: name.value,
                    email: email.value,
                    message: message.value
                })
            })

            const result = await response.json();


            if(result.success) {
                console.log(result);

                isLoading.value = false;
                notyf.success("Message Sent!")

                name.value = ""
                email.value = ""
                message.value = ""
            }
        }catch(err){
            console.log(err);
            isLoading.value = false;
            notyf.error("Failed to send message. Please try again")
        }
    }
</script>

<template>
    <div id="contact" class="my-5">
      <div class="container h-100">
        <div class="row d-flex align-items-center justify-content-center h-100">
          <h1 class="text-center">Contact</h1>
          <form @submit.prevent="submitForm" >
            <div class="col-12 p-5 rounded-4" id="form-border">
              <div class="mb-3">
                <label for="exampleFormControlInput1" class="form-label"
                  >Full Name</label
                >
                <input
                  type="text"
                  class="form-control"
                  id="exampleFormControlInput1"
                  placeholder="First Name M.I Last Name"
                  v-model="name"
                />
              </div>
              <div class="mb-3">
                <label for="exampleFormControlInput1" class="form-label"
                  >Email address</label
                >
                <input
                  type="email"
                  class="form-control"
                  id="exampleFormControlInput1"
                  placeholder="name@example.com"
                  v-model="email"
                />
              </div>
              <div class="mb-5">
                <label for="exampleFormControlTextarea1" class="form-label"
                  >Message</label
                >
                <textarea
                  class="form-control"
                  id="exampleFormControlTextarea1"
                  rows="3"
                  v-model="message"
                ></textarea>
              </div>
              <button type="submit" class="p-2 rounded-3" id="submit-button" :disabled="isLoading">
                {{ isLoading ? "Sending..." : "Submit" }}
              </button>
            </div>
          </form>
        </div>
      </div>
    </div>
</template>