<template>
   <base-card>
        <base-dialog title="Invalid Input" v-if="inputIsInvalid" @close="confirmBtn">
            <template #default>
                <p> A deserunt eaque nemo hic, id aliquam iusto.</p>
                <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Amet a magni quisquam aperiam impedit voluptas rem ratione, ab, harum voluptate modi nemo.</p>
            </template>
            <template #action>
                <base-button @click="confirmBtn">OK</base-button>
            </template>
        </base-dialog>
        <form @submit.prevent="addSubmit">
            <div class="form-control">
                <label for="title"> Title</label>
                <input type="text" id="title" ref="inputTitle" name="title">
            </div>
            <div class="form-control">
                <label for="description"> Description</label>
                <textarea name="description" id="description" cols="30" rows="10" ref="inputDes"></textarea>
            </div>
            <div class="form-control">
                <label for="link">Link</label>
                <input type="url" name="link" id="link" ref="inputLink">
            </div>
            <div class="form-control">
                <base-button type="submit">Submit</base-button>
            </div>
        </form>
    </base-card>
</template>
<script>
export default {
    inject : ['addRes'],
    data(){
        return {
            inputIsInvalid : false,
        }
    },
    methods:{
        addSubmit(){
            const enteredTitle = this.$refs.inputTitle.value;
            const enteredDes = this.$refs.inputDes.value;
            const enteredLink = this.$refs.inputLink.value;

            if(enteredTitle.trim() == '' || enteredDes.trim() == '' || enteredLink.trim() == ''){
                this.inputIsInvalid = true;
                return;
            }

            this.addRes(enteredTitle,enteredDes,enteredLink)

        },
        confirmBtn(){
            this.inputIsInvalid = false
        }
    }
}
</script>
<style scoped>
label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: 1px solid #ccc;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #3a0061;
  background-color: #f7ebff;
}

.form-control {
  margin: 1rem 0;
}
</style>