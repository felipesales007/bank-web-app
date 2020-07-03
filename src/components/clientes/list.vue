<template>
    <div class="row list-item">
        <div hidden class="cell" data-title="ID">{{ user.id}}</div>
        <div class="cell" data-title="Nome">{{ user.nome}}</div>
        <div class="cell" data-title="Agência">{{ user.agencia}}</div>
        <div class="cell" data-title="Conta">{{ user.conta}}</div>
        <div class="cell" data-title="Saldo"><span class="font-weight-bold">R$ {{ user.saldo.replace(".", ",") }}</span></div>
        <div class="cell" data-title="Ações">
            <button type="button" class="btn btn-primary mx-2" data-toggle="modal" data-target="#exampleModal" @click="onSacar">
                <i class="fas fa-arrow-up mr-2"></i>
                Sacar
            </button>
            <button type="button" class="btn btn-success mx-2" data-toggle="modal" data-target="#exampleModal" @click="onDepositar">
                <i class="fas fa-arrow-down mr-2"></i>
                Depositar
            </button>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'list',
        props: {
            user: {
                type: Object
            }
        },
        methods: {
            onSacar() {
                this.$emit("onSacar", this.user);
            },
            onDepositar() {
                this.$emit("onDepositar", this.user);
            }
        }
    };
</script>
