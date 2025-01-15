
#### 1. Interfaces

Em JavaScript, a maneira fundamental de agrupar e transmitir dados é através de objetos. No TypeScript, representamos esses _tipos de objeto_.

``` typescript
function greet(person: { name: string; age: number }) {

return "Hello " + person.name;

}
```

ou eles podem ser nomeados usando uma interface:

``` typescript
interface Person {

name: string;

age: number;

}

function greet(person: Person) {

return "Hello " + person.name;

}
```

ou usando type alias:

``` typescript
type Person = {

name: string;

age: number;

};

function greet(person: Person) {

return "Hello " + person.name;

}
```

##### Modificadores de Propriedade

Cada propriedade em um tipo de objeto pode especificar algumas coisas: o tipo, se a propriedade é opcional e se a propriedade pode ser gravada.

- **Propriedades opcionais:**  Você pode tornar uma propriedade opcional usando o `?`. Isso indica que a propriedade pode ou não estar presente no objeto. 

``` typescript
interface User {
  id: number;
  name?: string; // Opcional
}

const user1: User = { id: 1 };
const user2: User = { id: 2, name: "Eduardo" };

```

- **Propriedades somente leitura `(readonly)`**: Usando o modificador `readonly`, você pode tornar uma propriedade imutável após sua inicialização.

``` typescript
interface Config {
  readonly apiKey: string;
  url: string;
}

const config: Config = {
  apiKey: "12345",
  url: "https://api.example.com",
};

config.url = "https://api.newexample.com"; // Ok
config.apiKey = "67890"; // Erro: Não é possível alterar uma propriedade readonly

```


- **Extensão de interfaces com modificadores**: Você pode estender uma interface para adicionar modificadores adicionais às propriedades.

``` typescript
interface Basic {
  id: number;
  name: string;
}

interface Extended extends Basic {
  readonly isActive: boolean; // Propriedade somente leitura adicionada
  description?: string;       // Propriedade opcional adicionada
}

const extendedObject: Extended = {
  id: 1,
  name: "Eduardo",
  isActive: true,
};

extendedObject.isActive = false; // Erro: isActive é readonly

```


#### 2. Classes

As **classes** em TypeScript são uma forma de estruturar e organizar o código, fornecendo suporte a conceitos como herança, encapsulamento e polimorfismo, todos fundamentais no paradigma de programação orientada a objetos.

O TypeScript adiciona verificações de tipos e funcionalidades extras às classes do JavaScript, tornando-as mais seguras e poderosas.

##### Definição de uma classe

``` typescript
class Pessoa {
  nome: string;
  idade: number;

  constructor(nome: string, idade: number) {
    this.nome = nome;
    this.idade = idade;
  }

  cumprimentar(): string {
    return `Olá, meu nome é ${this.nome} e tenho ${this.idade} anos.`;
  }
}

const pessoa = new Pessoa("Eduardo", 20);
console.log(pessoa.cumprimentar());

```

##### Modificadores de acesso

Os modificadores de acesso controlam a visibilidade de membros (propriedades e métodos) dentro da classe.

1. `public` (Padrão): Os membros são acessíveis dentro e fora da classe.

``` typescript
class Carro {
  public marca: string;

  constructor(marca: string) {
    this.marca = marca;
  }

  public mostrarMarca(): void {
    console.log(`A marca do carro é ${this.marca}.`);
  }
}

const carro = new Carro("Toyota");
carro.mostrarMarca(); // Ok

```

2. `private`: Os membros só podem ser acessados dentro da própria classe.

``` typescript
class ContaBancaria {
  private saldo: number;

  constructor(saldoInicial: number) {
    this.saldo = saldoInicial;
  }

  public depositar(valor: number): void {
    this.saldo += valor;
  }

  public consultarSaldo(): number {
    return this.saldo;
  }
}

const conta = new ContaBancaria(100);
conta.depositar(50);
console.log(conta.consultarSaldo()); // 150
// conta.saldo = 1000; // Erro: 'saldo' é private
```

3. `protected`: Os membros são acessíveis dentro da classe e em subclasses:

``` typescript
class Animal {
  protected especie: string;

  constructor(especie: string) {
    this.especie = especie;
  }
}

class Cachorro extends Animal {
  public mostrarEspecie(): void {
    console.log(`O cachorro é da espécie: ${this.especie}`);
  }
}

const cachorro = new Cachorro("Canis lupus");
cachorro.mostrarEspecie(); // Ok
// cachorro.especie = "Gato"; // Erro: 'especie' é protected

```

##### Classes Abstratas

Classes abstratas servem como modelos e não podem ser instanciadas diretamente. Elas podem conter métodos abstratos (sem implementação) que devem ser definidos pelas subclasses.

``` typescript
abstract class Animal {
  abstract emitirSom(): void;

  mover(): void {
    console.log("O animal se moveu.");
  }
}

class Gato extends Animal {
  emitirSom(): void {
    console.log("Miau!");
  }
}

const gato = new Gato();
gato.emitirSom(); // Miau!
gato.mover();     // O animal se moveu.

```

#### Enum

No TypeScript, os **enums** são um recurso poderoso que permite definir um conjunto de valores nomeados. Esses valores podem ser numéricos ou baseados em strings.

1. **Enums Numéricos:** Por padrão, os enums numéricos atribuem valores sequenciais iniciando em de `0`.

``` typescript
enum Direction {
  Up,     // 0
  Down,   // 1
  Left,   // 2
  Right,  // 3
}

let dir: Direction = Direction.Up;
console.log(dir); // Saída: 0
```

Também pode atribuir valores explícitos:

``` typescript
enum Direction {
  Up = 10,
  Down,   // 11
  Left,   // 12
  Right,  // 13
}

console.log(Direction.Down); // Saída: 11

```


2.  **Enums Baseados em Strings**: Os enums de string precisam que cada membro tenha um valor explícito atribuído, mas são muito úteis para representar valores constantes.

``` typescript
enum Direction {
  Up = "UP",
  Down = "DOWN",
  Left = "LEFT",
  Right = "RIGHT",
}

let dir: Direction = Direction.Left;
console.log(dir); // Saída: LEFT

```


#### Tuplas

No TypeScript, **tuplas** são um tipo especial de array com um número fixo de elementos, onde cada elemento pode ter um tipo específico. Diferente de arrays normais, tuplas permitem definir a quantidade de elementos e seus tipos de forma explícita.

``` typescript
let user: [number, string];

// Atribuindo valores
user = [1, "Eduardo"]; // OK
// user = ["Eduardo", 1]; // Erro: Tipos na ordem errada
```


#### Objetos

Além dos primitivos, o tipo mais comum de tipo que você encontra é um _tipo de objeto_. Isso se refere a qualquer valor JavaScript com propriedades, que é quase todos eles! Para definir um tipo de objeto, simplesmente listamos suas propriedades e seus tipos.

**Por exemplo:** 

``` typescript
function printCoord(pt: { x: number; y: number }) {

console.log("The coordinate's x value is " + pt.x);

console.log("The coordinate's y value is " + pt.y);

}

printCoord({ x: 3, y: 7 });
```


Aqui, anotamos o parâmetro com um tipo com duas propriedades - x e y - que são ambas do tipo number. ==Você pode usar , ou ; para separar as propriedades, e o último separador é opcional de qualquer forma.== 

A parte do tipo de cada propriedade também é opcional. Se você não especificar um tipo, ele será assumido como any.


**Propriedades opcionais**

Os tipos de objeto também podem especificar que algumas propriedades são opcional. Para fazer isso, adicione um `?` após o nome da propriedade.

**Por exemplo:**

``` typescript
function printName(obj: { first: string; last?: string }) {

// ...

}

// Both OK

printName({ first: "Bob" });

printName({ first: "Alice", last: "Alisson" });
```

Em Javascript, se você acessar uma propriedades que não existe, você receberá o valor `undefined`em vez de um erro de tempo de execução. Por causa disso, quando você ler a partir de uma propriedade opcional, você terá que verificar `undefined` antes de usá-lo.

``` typescript
function printName(obj: { first: string; last?: string }) {

// Erro - pode travar se 'obj.last' não for fornecido!

console.log(obj.last.toUpperCase());

// 'obj.last' is possibly 'undefined'.'obj.last' is possibly 'undefined'.

if (obj.last !== undefined) {

// OK

console.log(obj.last.toUpperCase());

}

// Uma alternativa segura usando sintaxe JavaScript moderna:

console.log(obj.last?.toUpperCase());

}
```

