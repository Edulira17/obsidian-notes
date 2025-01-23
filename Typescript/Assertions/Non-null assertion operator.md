 No Typescript o operador `(!)` é uma funcionalidade que permite ao desenvolvedor informar ao compilador que um valor não será `null` ou `undefined` naquele ponto do código, mesmo que o Typescript não consiga garantir sozinho.

  Ele é representado por um ponto de exclamação `(!)` colocado logo após a variável ou expressão.

![[Pasted image 20250115121222.png]]

#### Quando usar o Non-null Assertion Operator ?

Ele é usado em situações onde você, como desenvolvedor, tem certeza de que o valor não será `null` ou `undefined`, mas o TypeScript não consegue inferir isso por conta própria.

#### Exemplos de Uso

1. **Acessando Elementos do DOM:**
    
    - Ao usar métodos como `document.querySelector`, o TypeScript infere que o resultado pode ser `Element | null`, o que exige uma verificação. Com `!`, você pode informar ao TypeScript que tem certeza de que o elemento existe.

``` typescript
const inputElement = document.querySelector("input")!;
inputElement.value = "Olá!";
```

Sem o `!`, seria necessário verificar se o elemento não é `null`:

``` typescript
const inputElement = document.querySelector("input");
if (inputElement) {
  inputElement.value = "Olá!";
}
```


#### Cuidados ao Usar o Non-null Assertion Operator

1. **Risco de Erros em Tempo de Execução:**

- Se você usar `!` em um valor que realmente for `null` ou `undefined`, isso resultará em um erro em tempo de execução.
	
``` typescript
let texto: string | null = null;
console.log(texto!.toUpperCase()); // Runtime Error: Cannot read property 'toUpperCase' of null
```

2. **Não é uma substituição para boas práticas:**

- Sempre que possível, prefira validar explicitamente os valores antes de usá-los, em vez de confiar cegamente no operador `!`.
	
``` typescript
// Verificando se a variável "texto" não é null ou undefined
if (texto) {
  console.log(texto.toUpperCase());
}
```


