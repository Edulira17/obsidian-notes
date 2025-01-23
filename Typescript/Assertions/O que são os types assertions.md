**Type assertions** no TypeScript são uma forma de informar ao compilador que sabemos mais sobre o tipo de uma variável do que ele consegue inferir. Em outras palavras, você está "afirmando" ao TypeScript qual é o tipo de uma variável em um determinado contexto, mesmo que ele não seja capaz de deduzir isso por conta própria.

Elas não alteram o tipo em tempo de execução (pois o TypeScript é uma linguagem de tipagem estática e não interfere em tempo de execução), mas ajudam a evitar erros de compilação quando temos certeza do tipo.

### Sintaxe de Type Assertions

Existem duas formas de escrever uma type assertion no TypeScript:

1. **Com a palavra-chave `as`**:
``` typescript
let valor: any = "123";
let tamanho: number = (valor as string).length;
console.log(tamanho); // Saída: 3	
```

2. **Com a sintaxe de "casting" (menos comum e não recomendada em JSX)**:
``` typescript
let valor: any = "123";
let tamanho: number = (<string>valor).length;
console.log(tamanho); // Saída: 3
```

==**Nota:== O uso de `as` é preferido, especialmente ao trabalhar com arquivos `.tsx` (React), porque a sintaxe `<string>` pode conflitar com a sintaxe de JSX**


## Const Assertions

As **const assertions** no TypeScript são uma funcionalidade que permite declarar que uma expressão deve ser tratada como imutável, tornando-a o mais específica possível. Elas são usadas ao final de uma declaração, utilizando o operador `as const`.

Isso transforma a estrutura para tipos literais "constantes", restringindo alterações nos valores ou propriedades.

 **O que `as const` faz?**

1. **Literal Narrowing (Restringe valores):**
    
    - Sem `as const`, o TypeScript infere tipos mais amplos como `string`, `number` ou `boolean`.
    - Com `as const`, ele infere os valores literais exatos.

``` typescript
let status = "ativo"; // Inferido como string
let statusLiteral = "ativo" as const; // Inferido como "ativo"
```


**Imutabilidade de propriedades:**

- Com `as const`, objetos e arrays tornam-se somente leitura (`readonly`).

``` typescript
const usuario = {
  nome: "Eduardo",
  idade: 20,
} as const;

usuario.nome = "Lira"; // Erro: Não é possível atribuir porque a propriedade é somente leitura.
```


## Satisfies Keyword Operator

O operador **`satisfies`** no TypeScript é uma funcionalidade poderosa introduzida no TypeScript 4.9. Ele é usado para garantir que um valor satisfaça os requisitos de um tipo, mas sem restringir o valor explicitamente a esse tipo.


#### O que é o `satisfies`?

O `satisfies` permite:

1. **Validar um valor em relação a um tipo:** Garante que o valor fornecido esteja em conformidade com a estrutura esperada.
2. **Preservar inferência mais específica do valor:** Ao contrário de uma anotação explícita de tipo, ele mantém os detalhes mais específicos do valor.

**Sintaxe do satisfies:**

``` typescript
const valor = { propriedade: "valor" } satisfies TipoEsperado;
```


#### Diferença entre `satisfies` e a Anotação de Tipo

1. `as` ou Anotação Explícita de Tipo:	
	Quando usamos um tipo explícito, o TypeScript **trunca** a inferência para corresponder ao tipo declarado.
	
``` typescript
type Config = { modo: "escuro" | "claro"; timeout: number };

const config: Config = { modo: "escuro", timeout: 3000, extra: true }; // Erro: "extra" não existe em "Config".
```

2. Com `satisfies`:
	Ele valida o tipo sem descartar informações adicionais ou restringir a inferência:
	
``` typescript
type Config = { modo: "escuro" | "claro"; timeout: number };

const config = { modo: "escuro", timeout: 3000, extra: true } satisfies Config;

console.log(config.extra); // OK: Informações adicionais são preservadas.
```
