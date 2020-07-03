<!-- app -->
<template>
    <div id="app">
        <clientes :users="users" @onSacar="onSacar" @onDepositar="onDepositar" />
        <modal :form="form" :modal="modal" @onFormSubmit="onFormSubmit" />
    </div>
</template>

<script>
    import axios from "axios";
    import clientes from './components/clientes/clientes';
    import modal from './components/clientes/modal';

    export default {
        name: 'App',
        components: {
            clientes,
            modal
        },
        data() {
            return {
                url: "http://localhost/bank/web-api/public/api/users",
                users: [],
                form: { valor: "" },
                modal: { titleModal: "", btnClass: "" }
            };
        },
        methods: {
            getUsers() {
                axios.get(this.url).then(data => {
                    this.users = data.data;
                });
            },
            editUser(data) {
                if (data.isSacar) {
                    if (parseFloat(data.saldo) >= parseFloat(data.valor)) {
                        data.valor = parseFloat(data.saldo) - parseFloat(data.valor);
                    } else {
                        alert('valor superior ao saldo disponivel');
                        return false;
                    }
                } else {
                    data.valor = parseFloat(data.saldo) + parseFloat(data.valor);
                }

                axios
                    .put(`${this.url}/${data.id}`, {
                        valor: data.valor
                    })
                    .then(() => {
                        this.getUsers();
                    })
                    .catch(e => {
                        alert(e);
                    });
            },
            onSacar(data) {
                this.form = data;
                this.form.isSacar = true;
                this.modal.titleModal = 'Sacar';
                this.modal.btnClass = 'btn btn-primary';
            },
            onDepositar(data) {
                this.form = data;
                this.form.isSacar = false;
                this.modal.titleModal = 'Depositar';
                this.modal.btnClass = 'btn btn-success';
            },
            onFormSubmit(data) {
                this.editUser(data);
            },
        },
        created() {
            this.getUsers();
        }
    };
</script>

<style>
    @font-face {
        font-family: Poppins-Regular;
        src: url(https://colorlib.com/etc/tb/Table_Responsive_v2/fonts/poppins/Poppins-Regular.ttf)
    }

    @font-face {
        font-family: Poppins-Bold;
        src: url(https://colorlib.com/etc/tb/Table_Responsive_v2/fonts/poppins/Poppins-Bold.ttf)
    }

    #app {
        font-family: Poppins-Regular, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
    }
</style>
