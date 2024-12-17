    <script setup>

        import { ref, watch } from 'vue';

        // Variáveis reativas que servem para qualquer mudança de valor no caso da conta ele muda automaticamente
        const numero1 = ref(0);
        const numero2 = ref(0);
        const operacao = ref('+');
        const resultado = ref(0);

        // Função de cálculo
        const calcular = () => {
        let res = 0;

        switch (operacao.value) {
            case '+':
            res = numero1.value + numero2.value;
            break;
            case '-':
            res = numero1.value - numero2.value;
            break;
            case '*':
            res = numero1.value * numero2.value;
            break;
            case '/':
            if (numero2.value === 0) {
                console.log("Erro: Divisão por zero não é permitida.");
                res = "Indefinido"; 
            } else {
                res = numero1.value / numero2.value;
            }
            break;
            default:
            res = 'Operação inválida';
        }

        resultado.value = typeof res === 'number' ? res.toFixed(2) : res;
        };

        // Observa mudanças nos inputs e recalcula automaticamente
        watch([numero1, numero2, operacao], calcular);

        </script>

        <template>

        <div>
            <div class="calculadora">
            <form @submit.prevent="calcular">
            <div>
                <label for="numero-1">Número 1:</label>
                <input type="number" id="numero-1" v-model.number="numero1" />
            </div>

            <div>
                <label for="numero-2">Número 2:</label>
                <input type="number" id="numero-2" v-model.number="numero2" />
            </div>

            <div>
                <label for="selecao">Operação:</label>
                <select id="selecao" v-model="operacao">
                <option value="+">+</option>
                <option value="-">-</option>
                <option value="*">*</option>
                <option value="/">/</option>
                </select>
            </div>

            </form>

            <div>
            <label for="resultado" id="">Resultado:</label>
            <input type="text" id="resultado" :value="resultado" readonly />
            </div>
        </div>

        </div>

        </template>

        <style scoped>

      

    body {
        font-family: 'Arial', sans-serif;
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh;
        margin: 0;
    }
  


    div.calculadora {
        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: column; 
        width: 100%; 
        max-width: 400px; 
        margin-top: 210px; 
        margin-left: 700px;
    }


    form {
        background-color: rgba(255, 255, 255, 0.9); 
        padding: 25px;
        border-radius: 12px;
        box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2); 
        width: 100%; 
        color: #333333; 
        text-align: center; /* Centraliza o texto */
        display: flex;
        flex-direction: column; /* Organiza os elementos em coluna */
        align-items: center; /* Centraliza horizontalmente */
    }

    /* Controle de cada campo do formulário */
    .form-control {
        display: flex;
        flex-direction: column;
        margin-bottom: 20px;
        width: 100%; /* Garante que ocupe toda a largura */
    }

    /* Ajuste para os rótulos */
    label {
        margin-bottom: 10px;
        font-weight: bold;
        color: #333333; /* Cor do texto */
        text-align: left; /* Alinha o texto à esquerda */
        width: 100%; /* Ocupa toda a largura */
    }

    /* Estilo para campos de entrada e seleção */
    input, select {
        padding: 12px;
        font-size: 16px;
        border: 1px solid #ddd;
        border-radius: 6px;
        width: 100%;
        box-sizing: border-box; /* Garante que o padding não ultrapasse a largura */
        text-align: center; /* Centraliza o texto dentro do campo */
    }

    /* Muda a cor de fundo do campo de resultado */
    input[readonly] {
        background-color: #f1f1f1;
        color: #555;
        cursor: not-allowed; /* Cursor indica que o campo não pode ser editado */
    }

    /* Estilo do botão */
    button {
        margin-top: 20px;
        padding: 12px 24px;
        font-size: 18px;
        color: #ffffff;
        background-color: #0984e3; /* Azul vibrante */
        border: none;
        border-radius: 6px;
        cursor: pointer;
        width: 100%;
        text-align: center;
        transition: background-color 0.3s ease; /* Transição suave para hover */
    }

    /* Efeito ao passar o mouse no botão */
    button:hover {
        background-color: #074cad; /* Azul mais escuro */
    }

    /* Texto centralizado e espaçamento */
    form h1 {
        text-align: center;
        margin-bottom: 25px;
        color: #333;
        font-size: 1.8em;
        font-weight: bold;
    }
    </style>
