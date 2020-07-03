<template>
    <!-- modal -->
    <div class="modal fade" id="exampleModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
        <div class="modal-dialog modal-sm" role="document">
            <div class="modal-content">
                <!-- título -->
                <div class="modal-header">
                    <h5 class="modal-title" id="exampleModalLabel">{{ modal.titleModal }} valor</h5>
                    <button type="button" class="close text-danger" data-dismiss="modal" aria-label="Close">
                        <span aria-hidden="true">&times;</span>
                    </button>
                </div>

                <!-- formulário -->
                <form>
                    <!-- corpo -->
                    <div class="modal-body">
                        <input type="number" id="valor" name="valor" class="form-control" placeholder="R$" @change="handleChanger" :value="form.valor">
                    </div>
                    <!-- botões -->
                    <div class="modal-footer">
                        <button type="button" class="btn btn-danger" data-dismiss="modal">
                            <i class="fas fa-times mr-2"></i>
                            Fechar
                        </button>
                        <button type="submit" :class="modal.btnClass" @click="onFormSubmit">
                            <i class="fas fa-check mr-2"></i>
                            {{ modal.titleModal }}
                        </button>
                    </div>
                </form>
            </div>
        </div>
    </div>
</template>

<script>
    export default  {
        name: 'modal',
        props: {
            modal: Object,
            form: Object
        },
        methods: {
            handleChanger(event) {
                const { name, value } = event.target;
                let form = this.form;
                form[name] = value;
                this.form = form;
            },
            onFormSubmit(e) {
                e.preventDefault();

                if (this.formValidation()) {
                    this.$emit('onFormSubmit', this.form);
                    document.querySelector('.close').click();
                    this.clearFormFields();
                }
            },
            formValidation() {
                if (document.getElementsByName('valor')[0].value === '') {
                    alert('Valor obrigatório');
                    return false;
                }

                return true;
            },
            clearFormFields() {
                this.form.valor = '';
                document.querySelector('form').reset();
            }
        }
    };
</script>
