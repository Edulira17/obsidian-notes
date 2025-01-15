No TypeScript, o tipo `unknown` é chamado de **"top type"** (tipo mais abrangente) porque, assim como `any`, ele pode representar **qualquer tipo de valor**. No entanto, ao contrário de `any`, o `unknown` mantém a segurança de tipos, exigindo que você faça verificações explícitas antes de operar com o valor.

### Principais características do `unknown`:

1. **Representa qualquer tipo**:
    
    - Uma variável declarada como `unknown` pode conter valores de qualquer tipo (string, number, object, etc.).
2. **Mais seguro que `any`**:
    
    - O TypeScript não permite que você utilize o valor de uma variável `unknown` diretamente sem antes verificar o tipo.
    - Isso reduz a chance de erros de tempo de execução, forçando você a garantir que o valor seja do tipo esperado antes de manipulá-lo.
3. **Força verificações de tipo explícitas**:
    
    - Antes de acessar propriedades ou métodos em uma variável `unknown`, você precisa confirmar que o tipo é compatível.

``` typescript
let valor: unknown;

valor = 42;              // Pode ser um número
valor = "Olá, mundo!";   // Pode ser uma string
valor = { nome: "Eduardo" }; // Pode ser um objeto

// Não é possível acessar diretamente propriedades ou métodos
// console.log(valor.toUpperCase()); // ERRO: valor é do tipo 'unknown'

// É necessário verificar o tipo antes de usar
if (typeof valor === "string") {
  console.log(valor.toUpperCase()); // Funciona porque foi verificado que é uma string
}

if (typeof valor === "number") {
  console.log(valor.toFixed(2)); // Funciona porque foi verificado que é um número
}

```

