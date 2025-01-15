
#### 1. **String, Number e Boolean**

JavaScript tem três muito comumente usados [primitivos](https://developer.mozilla.org/en-US/docs/Glossary/Primitive): `string`, `number` e `boolean`. Cada um tem um tipo correspondente no TypeScript. Como você pode esperar, estes são os mesmos nomes que você pode ver se você usou o JavaScript `typeof` operador em um valor desses tipos:

#### 2. **Void**

`void` é um tipo que indica a ausência de um valor. Ele é comumente usado em funções que não retornam nenhum valor.

``` typescript
function logMessage(message: string): void {
  console.log(message);
}
```

##### Diferença entre `void` e `undefined`:

Embora uma função com retorno `void` não deva retornar nenhum valor útil, ela ainda pode retornar `undefined` implicitamente.

``` typescript
function doNothing(): void {
  // Não retorna nada explicitamente.
}

const result = doNothing();
console.log(result); // undefined

```

#### 3. null

JavaScript tem dois valores primitivos usados para sinalizar valor ausente ou não inicializado: `null` (ausente) e `undefined` (não-inicializado).

TypeScript tem dois correspondentes _tipos_ pelos mesmos nomes. Como esses tipos se comportam depende se você tem o `strictNullChecks`.

##### Por que usar `strictNullChecks`?

Por padrão, em Typescript sem o `strictNullChecks`, todos os tipos podem aceitar `null` e `undefined`. Isso pode levar a erros imprevisíveis em tempo de execução. Com o `strictNullChecks` ativado, você precisa lidar explicitamente com `null` e `undefined`, tornando seu código mais seguro e previsível.

##### Como ativar `strictNullChecks`?

``` json
{
  "compilerOptions": {
    "strictNullChecks": true
  }
}
```





