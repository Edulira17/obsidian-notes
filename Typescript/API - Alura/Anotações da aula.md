### **Seção 2**

- Criar um tipo personalizado (TipoPet) para representar pets com campos específicos;
- Introduzir uma enumeração (EnumEspecie) para limitar as opções de espécie para "cachorro" e "gato";
- Substituir o campo "idade" por "dataDeNascimento" para fornecer dados mais precisos e deixar o cálculo da idade para os consumidores da API.

### **Seção 3**

#### **O que é TypeORM ?**

TypeORM é um ORM que permite aos desenvolvedores trabalhar com bancos de dados relacionais usando uma abordagem orientada a objetos. Ele é escrito em TypeScript e foi projetado para ser usado com Node.js. O TypeORM suporta os principais bancos de dados, incluindo MySQL, PostgreSQL, MariaDB, SQLite, e até mesmo Microsoft SQL Server.

Com TypeORM, você pode definir entidades e relacionamentos diretamente no seu código TypeScript, permitindo uma integração perfeita entre a lógica da aplicação e o banco de dados. Ele também oferece suporte a migrações de banco de dados, permitindo que você mantenha o esquema do banco de dados sincronizado com o código da sua aplicação.

### Instalação do TypeORM:

1. Instalando o pacote NPM:  `npm install typeorm --save

2. Você precisa instalar `reflect-metadata`: `npm install reflect-metadata --save`
	e importe-o em algum lugar no local global do seu aplicativo (por exemplo, em `app.ts`): `import "reflect-metadata"`

3. Talvez precise instalar os tipos do Node para permitir recursos de tipagem do Typescript: `npm install @types/node --save-dev`


#### Conectando o Banco de Dados na minha aplicação:

Vamos criar o nosso datasource, uma configuração que permite que sua aplicação Node.js se conecte e interaja com um banco de dados, incluindo informações como tipo de banco, host e credenciais de acesso.

```javascript
import "dotenv/config";
import "reflect-metadata";
import { DataSource } from "typeorm";
import PetEntity from "../entities/PetEntity";

export const AppDataSource = new DataSource({
  type: "sqlite",
  database: "./src/config/database.sqlite", // caminho para o arquivo do banco de dados SQLite
  synchronize: true,
  logging: false,
  entities: [PetEntity], //todas as entidades da aplicação devem ser inseridas aqui
  migrations: [],
  subscribers: [],
});
```


- `entities`: define as entidades que serão mapeadas para tabelas no banco de dados. No exemplo, apenas a entidade `PetEntity` está definida para ser usada.
    
- `type`: define o tipo de banco de dados, que é "sqlite" neste caso, indicando que um banco de dados SQLite será usado.
    
- `database`: especifica o caminho para o arquivo do banco de dados SQLite que será criado/usado, localizado em "./src/config/database.sqlite".
    
- `synchronize`: quando definido como `true`, permite que o TypeORM crie automaticamente as tabelas do banco de dados com base nas entidades definidas. É útil durante o desenvolvimento, ==mas deve ser desativado em produção para evitar perda de dados acidentais.==
    
- `logging`: quando definido como `false`, desativa a saída de log do TypeORM, impedindo que mensagens de log sejam impressas no console, o que serve para manter o ambiente de produção mais limpo e seguro.

### Seção 4

#### Tipos utilitários do TypeScript vs. Campos opcionais

Os tipos utilitários no TypeScript são ferramentas poderosas para manipulação de tipos. Eles ajudam a criar tipos derivados com base em tipos existentes, tornando o desenvolvimento mais eficiente e seguro.

1 - **`Partial<Type>` vs. Campos Opcionais**

- O tipo `Partial<Type>` é usado para criar um tipo que faz com que todas as propriedades de `Type` sejam opcionais. Isso é útil quando você deseja criar uma versão parcial de um objeto com alguns campos opcionais.


**Exemplo com `Partial<Type>`:**

```typescript
interface Pessoa {
  nome: string;
  idade: number;
  email?: string;
}

type PessoaOpcional = Partial<Pessoa>;

const pessoa: PessoaOpcional = { nome: "Alice" }; // Todos os campos são opcionais
```

**Exemplo com campos opcionais:**

```typescript
interface Pessoa {
  nome: string;
  idade?: number; // Tornando a idade opcional
  email?: string; // Uso de campo opcional
}

const pessoa: Pessoa = { nome: "Alice" }; // Uso de campo opcional
```


**A principal diferença é que `Partial<Type>` permite que você defina a opcionalidade em um nível mais granular, enquanto campos opcionais são definidos individualmente nas propriedades.**


2 - **Pick<Type, Keys> vs. Omissão de Propriedades**

- O tipo `Pick<Type, Keys>` permite criar um tipo que contém apenas as propriedades especificadas por `Keys` de `Type`. Isso pode ser útil para criar tipos que incluem apenas um subconjunto das propriedades de um objeto.

**Exemplo com `Pick<Type>`:**

```typescript
interface Pessoa {
  nome: string;
  idade: number;
  email: string;
}

type InfoPessoal = Pick<Pessoa, "nome" | "idade">;

const info: InfoPessoal = { nome: "Bob", idade: 30 };
```

Neste exemplo acima, `PessoaSelecionada` conterá apenas as propriedades "nome" e "idade" do tipo `Pessoa`.



**Exemplo com omissão de propriedades:**

```typescript
   interface Pessoa {
     nome: string;
     idade: number;
     email: string;
   }

   type InfoPessoal = { nome: string; idade: number }; // Escolhendo propriedades diretamente

   const info: InfoPessoal = { nome: "Bob", idade: 30 };
```

**Ambos os métodos permitem criar tipos com um subconjunto de propriedades, mas `Pick<Type>` é mais conveniente quando você precisa selecionar várias propriedades de uma só vez.**


3 - **Exclude<Type, ExcludedUnion> vs. Exclusão de Valores**

- O tipo `Exclude<Type, ExcludedUnion>` permite criar um tipo que exclui todos os membros de `ExcludedUnion` do `Type`. Isso pode ser útil para criar tipos que excluem valores específicos de um tipo de união.

**Exemplo com `Exclude<Type>`:**

```typescript
type Cor = "vermelho" | "verde" | "azul";
type CoresExcluidas = Exclude<Cor, "vermelho" | "verde">;

const cor: CoresExcluidas = "azul"; // "azul" é o único valor permitido
```

**Neste exemplo acima, `CoresExcluidas` conterá apenas "azul", pois "vermelho" e "verde" foram excluídos da união de tipos `Cores`.**


**Exemplo de exclusão de valores:**

```typescript
type Cor = "vermelho" | "verde" | "azul";
type CoresExcluidas = "azul"; // Exclusão direta de valores

const cor: CoresExcluidas = "azul"; // "azul" é o único valor permitido
```

**Ambos os métodos alcançam o mesmo resultado, mas `Exclude<Type>` pode ser mais flexível quando você deseja excluir vários valores de uma só vez.**

**Essas comparações destacam como os tipos utilitários do TypeScript podem ser convenientes e flexíveis em relação aos campos opcionais e outras operações de tipos no TypeScript.**

**Cada abordagem tem suas vantagens, e a escolha depende das necessidades específicas do seu código.**


#### Perguntinha

![[Pasted image 20250106122549.png]]