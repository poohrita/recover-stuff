<template>
    <div>
        Hello {{ name }}: {{ formTark }}


        <form v-if="updateTark" @submit.prevent="updatedTark">
            <input type="text" v-model="formTark">
            <button type="submit">update Tark</button>
        </form>

        <form v-else @submit.prevent="saveTark">
            <input type="text" v-model="formTark">
            <button type="submit">Save</button>
        </form>

        <ul>
            <li v-for="(item, index) in tarks" :key="index">
                {{ item.name }}

                <button type="button" @click="editTark(item.id)">edit</button>
            </li>
        </ul>
    </div>
</template>

<script>

export default {
    data() {
        const tarks = [];

        return {
            name: `Chong`,

            tarks,

            formTark: '',
            updateTark: null,

            curentIndex: 0
        }
    },

    methods: {
        saveTark() {


            if (!this.formTark == '') {

                this.curentIndex++;
                this.tarks.push({ id: this.curentIndex, name: this.formTark })

                this.updateTark = null;
                this.formTark = '';
            }

        },

        editTark(id) {
            const tark = this.findTarkById(id)

            this.updateTark = tark
            this.formTark = tark.name
        },

        findTarkById(id) {
            return this.tarks.find(item => item.id == id)
        },

        updatedTark() {
            console.log('updatedTark...');

            const tark = this.findTarkById(this.updateTark.id)

            tark.name = this.formTark
            this.updateTark = null
        },
    },
}
</script>