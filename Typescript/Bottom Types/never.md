No TypeScript, o tipo `never` é um tipo especial que representa **valores que nunca ocorrem**. Ele é usado em situações onde uma função, variável ou expressão não pode produzir um valor ou atingir um estado válido.


### Principais características do `never`:

1. **Representa ausência de valor**:
    
    - Diferente de `void` (que representa a ausência de retorno em funções), o `never` indica que **nenhum valor será retornado**, nem mesmo `undefined`.
2. **Usado em cenários de impossibilidade lógica**:
    
    - Funções que **lançam erros** ou **entram em loops infinitos**.
    - Situações onde um código deveria ser **inacessível**.
3. **Subtipo de todos os tipos**:
    
    - O `never` pode ser atribuído a qualquer tipo, mas nenhum tipo pode ser atribuído a `never` (exceto o próprio `never`).

**Exemplo de uso**:

``` typescript
function throwError(message: string): never {
  throw new Error(message); // Lança um erro, não retorna nada
}

function infiniteLoop(): never {
  while (true) {
    // Loop infinito, nunca sai daqui
  }
}

```


**Diferenças entre `never` e outros tipos**

|**Tipo**|**Descrição**|
|---|---|
|`void`|Usado em funções que **não retornam um valor** explícito (retornam `undefined` por padrão).|
|`undefined`|Representa a ausência de um valor atribuído a uma variável.|
|`null`|Representa um valor nulo explícito (sem referência a nenhum objeto).|
|`never`|Indica que **não pode haver retorno ou valor**, usado em cenários como erros ou código inalcançável.|