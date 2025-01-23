**Type Inference** (inferência de tipos) é o mecanismo do TypeScript que permite ao compilador deduzir automaticamente o tipo de uma variável, função ou expressão, sem que você precise anotá-lo explicitamente. Isso melhora a produtividade e mantém a segurança do tipo, evitando declarações redundantes.

### **Como a Type Inference Funciona?**

O TypeScript analisa o código para determinar qual tipo faz mais sentido com base no contexto. Ele deduz o tipo:

1. **A partir do valor atribuído a uma variável.**
2. **A partir do valor retornado por uma função.**
3. **A partir do uso de expressões.**

### **Exemplos de Type Inference**

1. **Inferência em Variáveis:**
	
``` typescript
let nome = "Eduardo"; // Inferido como string
let idade = 20;       // Inferido como number
let ativo = true;     // Inferido como boolean
```

O TypeScript deduz os tipos com base nos valores atribuídos. Após a inferência:

- `nome` será do tipo `string`.
- `idade` será do tipo `number`.
- `ativo` será do tipo `boolean`

Se você tentar atribuir outro tipo, o Typescript gera um erro:

``` typescript
nome = 123; // Erro: Type 'number' não pode ser atribuído ao tipo 'string'.
```


