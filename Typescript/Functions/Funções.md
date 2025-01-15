As funções são o principal meio de transmitir dados em JavaScript. TypeScript permite que você especifique os tipos de ambos os valores de entrada e saída de funções.

**Tipo de Parâmetro Anotações**

Ao declarar uma função, você pode adicionar anotações de tipos após  cada parâmetro para declarar quais tipos de parâmetros a função aceita. Anotações do tipo parâmetro vão depois do nome do parâmetro: 

``` typescript
// Parameter type annotation

function greet(name: string) {

console.log("Hello, " + name.toUpperCase() + "!!");

}
```

``` typescript
// Would be a runtime error if executed!

greet(42);
----------
//Argument of type 'number' is not assignable to parameter of type 'string'.
```


**Anotações de tipo de retorno**

Você também pode adicionar anotações de tipo de retorno. Anotações de tipo de retorno aparecem após a lista de parâmetros:

``` typescript
function getFavoriteNumber(): number {

return 26;

}
```

Assim como as anotações de tipo de variável, você normalmente não precisa de uma anotação de tipo de retorno porque o TypeScript inferirá o tipo de retorno da função com base em suas instruções de retorno. A anotação de tipo no exemplo acima não altera nada. Algumas bases de código especificarão explicitamente um tipo de retorno para fins de documentação, para evitar alterações acidentais ou apenas por preferência pessoal.


**Funções que retornam Promises**:

Se você quiser anotar o tipo de retorno de uma função que retorna uma promessa, você deve usar o `Promise` tipo:

``` typescript
async function getFavoriteNumber(): Promise<number> {

return 26;
```


**Funções Anônimas:**

Funções anônimas são um pouco diferentes de declarações de função. Quando uma função aparece em um lugar onde o TypeScript pode determinar como ela será chamada, os parâmetros dessa função recebem tipos automaticamente.

``` typescript
const names = ["Alice", "Bob", "Eve"];

// Contextual typing for function - parameter s inferred to have type string

names.forEach(function (s) {

console.log(s.toUpperCase());

});

// Contextual typing also applies to arrow functions

names.forEach((s) => {

console.log(s.toUpperCase());

});
```
