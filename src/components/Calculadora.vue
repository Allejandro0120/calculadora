<template>
    <v-container class="d-flex flex-column justify-center align-center">
        <v-card class="card-visor">
            <v-card-text>
                <v-text-field
                    rounded
                    hide-details
                    v-model="valor"
                    height="60px"
                    dark
                    readonly
                >
                </v-text-field>
            </v-card-text>
        </v-card>
        <v-card class="card-calculadora">
            <v-card-text class="card_container_calculadora">
                    <v-btn class="button_calculadora" rounded @click="addToModel('7')">7</v-btn>
                    <v-btn class="button_calculadora" rounded @click="addToModel('8')">8</v-btn>
                    <v-btn class="button_calculadora" rounded @click="addToModel('9')">9</v-btn>
                    <v-btn class="button_calculadora" rounded @click="preoperate('divide')">/</v-btn>
            </v-card-text>
            <v-card-text class="card_container_calculadora">
                    <v-btn class="button_calculadora" rounded @click="addToModel('4')">4</v-btn>
                    <v-btn class="button_calculadora" rounded @click="addToModel('5')">5</v-btn>
                    <v-btn class="button_calculadora" rounded @click="addToModel('6')">6</v-btn>
                    <v-btn class="button_calculadora" rounded @click="preoperate('multiply')">x</v-btn>
            </v-card-text>
            <v-card-text class="card_container_calculadora">
                    <v-btn class="button_calculadora" rounded @click="addToModel('1')">1</v-btn>
                    <v-btn class="button_calculadora" rounded @click="addToModel('2')">2</v-btn>
                    <v-btn class="button_calculadora" rounded @click="addToModel('3')">3</v-btn>
                    <v-btn class="button_calculadora" rounded @click="preoperate('minus')">-</v-btn>
            </v-card-text>
            <v-card-text class="card_container_calculadora">
                    <v-btn class="button_calculadora del_button" rounded @click="del()">DEL</v-btn>
                    <v-btn class="button_calculadora" rounded @click="addToModel('.')">.</v-btn>
                    <v-btn class="button_calculadora" rounded @click="addToModel('0')">0</v-btn>
                    <v-btn class="button_calculadora" rounded @click="preoperate('plus')">+</v-btn>
            </v-card-text>
            <v-card-text class="card_container_calculadora">
                    <v-btn class="button_calculadora_especial del_button" rounded @click="reset()">RESET</v-btn>
                    <v-btn class="button_calculadora_especial total_button" rounded @click="equal()">=</v-btn>
            </v-card-text>
        </v-card>
    </v-container>
</template>

<script>
export default {
    name: 'Calculadora',
    data() {
        return {
            valor: "",
            operando1: null,
            operando2: null,
            resultado: false,
            operation: null,
        }
    },
    methods: {
        addToModel(value) {
            if(!this.resultado) {
                if (this.valor === "" || this.valor === "0") {
                    this.valor = value;
                } else {
                    this.valor += value;
                }
            }
            else {
                this.operando1 = this.valor;
                this.valor = value;
            }
        },
        reset() {
            console.log("reset");
            this.valor = "";
            this.operando1 = null;
            this.operando2 = null;
        },
        del() {
            this.valor = this.valor.slice(0, -1);
        },
        preoperate(item) {
            if (this.operando1 === null) {
                this.operando1 = parseFloat(this.valor);
                this.valor = '';
            } else {
                if (this.valor != '' ) {
                    this.operando2 = parseFloat(this.valor);
                    this.operate();
                }
            }
            if (item === 'plus') this.operation = 'plus';
            if (item === 'minus') this.operation = 'minus';
            if (item === 'multiply') this.operation = 'multiply';
            if (item === 'divide') this.operation = 'divide';
        },
        operate() {
            if (this.operation === 'plus') {
                this.valor = (parseFloat(this.operando1) + parseFloat(this.operando2)).toString();
            }
            if (this.operation === 'minus') {
                this.valor = (parseFloat(this.operando1) - parseFloat(this.operando2)).toString();
            }
            if (this.operation === 'multiply') {
                this.valor = (parseFloat(this.operando1) * parseFloat(this.operando2)).toString();
            }
            if (this.operation === 'divide') {
                this.valor = (parseFloat(this.operando1) / parseFloat(this.operando2)).toString();
            }
            this.resultado = true
        },
        equal() {
            if (this.operation != null) {
                this.preoperate(this.operation);
            }
        }
    }
}
</script>

<style>
    .card-visor {
        width: 535px;
        height: 120px;
        background-color: hsl(224, 36%, 15%) !important;
;
    }

    .card-calculadora {
        width: 535px;
        height: 460px;
        margin-top: 50px;
        padding: 30px 0;
        background-color: hsl(223, 31%, 20%) !important;
    }

    .card_container_calculadora {
        width: 100%;
        display: flex;
        justify-content: space-around;
        align-items: center;
    }

    .v-btn {
        width: 20%;
        height: 50px !important;
        font-size: 30px !important;
    }

    .button_calculadora_especial {
        width: 45%;
    }

    .del_button {
        background-color: hsl(225, 21%, 49%) !important;
        color: #FFF !important;
    }

    .total_button {
        background-color: hsl(6, 63%, 50%) !important;
        color: #FFF !important;
    }

    .v-input input {
        font-size: 48px;
        max-height: 60px !important;
    }
</style>