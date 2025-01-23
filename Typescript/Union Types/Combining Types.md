
## Union Types

O **Union Type** no TypeScript é um recurso que permite declarar que uma variável, função ou propriedade pode assumir mais de um tipo específico. Ele é utilizado quando uma entidade pode conter um valor de diferentes tipos, proporcionando maior flexibilidade e segurança no código.

**Sintaxe:**
``` typescript
let variável: tipo1 | tipo2 | tipo3;
```

**Exemplo simples:**
``` typescript
let id: string | number;

id = 123;       // Válido
id = "ABC123";  // Válido
id = true;      // Erro: boolean não faz parte do union type
```


**Quando usar ?**

O Union Type é ideal quando:

 - Uma entidade pode representar diferentes tipos de dados, como identificadores que podem ser string ou  números.
 - Funções ou propriedades precisam aceitar múltiplos tipos de entrada.

**Vantagens:**

- **Flexibilidade:** Permite lidar com tipos sem perder a segurança de tipo.
- **Segurança:** O Typescript ainda verifica erros de tipo em tempo de desenvolvimento.

**Cuidados:**

- **Complexidade:** Excesso de union types pode tornar o código mais difícil de entender e manter.
- **Checagem de Tipos:** É  importante verificar o tipo da variável antes de usá-la, para evitar comportamentos inesperados.


## Type Intersection

O **Type Intersection** no TypeScript é um recurso que permite combinar múltiplos tipos em um único tipo. Ele é utilizado quando uma entidade precisa satisfazer os requisitos de dois ou mais tipos ao mesmo tempo. Esse recurso é representado pelo operador `&`.

**Sintaxe:**
``` typescript
type Tipo1 = { propriedade1: tipo };
type Tipo2 = { propriedade2: tipo };

type TipoCombinado = Tipo1 & Tipo2;
```

**Quando utilizamos a interseção de tipos, o resultado é um tipo que possui **todas as propriedades de ambos os tipos**.**

