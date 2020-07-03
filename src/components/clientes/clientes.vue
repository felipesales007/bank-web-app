<template>
    <!-- corpo -->
    <div class="container">
        <!-- tabela -->
        <div class="wrap-table">
            <div class="table">
                <!-- título -->
                <div class="row header bg-primary">
                    <div hidden class="cell">ID</div>
                    <div class="cell">Nome</div>
                    <div class="cell">Agência</div>
                    <div class="cell">Conta</div>
                    <div class="cell">Saldo</div>
                    <div class="cell"><i class="fas fa-cog"></i></div>
                </div>
                <!-- lista -->
                <list v-for="user in users" :key="user.id" :user="user" @onSacar="onSacar" @onDepositar="onDepositar" />
            </div>
        </div>
    </div>
</template>

<script>
    import List from "./list";

    export default {
        name: 'clientes',
        components: {
            List
        },
        props: {
            users: {
                type: Array
            }
        },
        methods: {
            onSacar(data) {
                this.$emit("onSacar", data);
            },
            onDepositar(data) {
                this.$emit("onDepositar", data);
            }
        }
    };
</script>

<style>
    .wrap-table {
        width: 100%;
        border-radius: 10px;
        border: 1px solid #eeeeee;
        overflow: hidden
    }

    .table {
        width: 100%;
        display: table;
        margin: 0
    }

    .row {
        display: table-row;
    }

    .cell {
        display: table-cell
    }

    .row .cell {
        font-family: Poppins-Regular, sans-serif;
        font-size: 15px;
        color: #666;
        line-height: 1.2;
        font-weight: unset !important;
        padding-top: 20px;
        padding-bottom: 20px;
        border-bottom: 1px solid #f2f2f2
    }

    .row.header .cell {
        font-family: Poppins-Regular, sans-serif;
        font-size: 18px;
        color: #fff;
        line-height: 1.2;
        font-weight: unset !important;
        padding-top: 19px;
        padding-bottom: 19px
    }

    .row .cell {
        padding-left: 40px
    }

    .table,
    .row {
        width: 100% !important
    }

    .row.list-item:hover {
        background-color: #ececff
    }

    button {
        margin: -20px;
    }

    @media screen and (max-width: 768px) {
        .row:hover {
            background-color: #ececff
        }

        .table {
            display: block
        }

        .row {
            display: block
        }

        .row.header {
            padding: 0;
            height: 0
        }

        .row.header .cell {
            display: none
        }

        .row .cell:before {
            font-family: Poppins-Bold, sans-serif;
            font-size: 12px;
            color: gray;
            line-height: 1.2;
            text-transform: uppercase;
            font-weight: unset !important;
            margin-bottom: 13px;
            content: attr(data-title);
            min-width: 98px;
            display: block
        }

        .cell {
            display: block
        }
    }

    @media (max-width: 768px) {
        .row {
            border-bottom: 1px solid #f2f2f2;
            padding-bottom: 18px;
            padding-top: 30px;
            padding-right: 15px;
            margin: 0
        }

        .row .cell {
            border: none;
            padding-left: 30px;
            padding-top: 16px;
            padding-bottom: 16px
        }

        .row .cell:nth-child(1) {
            padding-left: 30px
        }

        .row .cell {
            font-family: Poppins-Regular, sans-serif;
            font-size: 18px;
            color: #555;
            line-height: 1.2;
            font-weight: unset !important
        }

        .table,
        .row,
        .cell {
            width: 100% !important
        }
    }
</style>
