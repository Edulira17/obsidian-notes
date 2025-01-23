
#### O que são decorators ?

Decorators são funções especiais que podem ser anexadas a classes, métodos, propriedades ou parâmetros de função em TypeScript. Eles permitem que você adicione funcionalidades extras ou metadados a esses elementos sem modificar diretamente o código-fonte subjacente. Os decoradores são marcados com o símbolo `@` e são executados quando a classe ou método é definido.

#### Por que usar decorators ?

1. **Validação de Dados:** decorators podem ser usados para validar dados de entrada em uma classe, garantindo que os valores atendam a critérios específicos antes de serem armazenados.
    
2. **Controle de Acesso:** eles podem ser usados para definir permissões de acesso a métodos ou propriedades, garantindo que apenas usuários autorizados possam executá-los.
    
3. **Registro de Log:** decorators podem registrar informações úteis, como logs de tempo de execução, para fins de depuração e auditoria.
    
4. **Transformação de Dados:** Eles permitem que você transforme dados antes de serem processados, tornando-os versáteis para adaptação a diferentes cenários.


#### Explorando Decorators com TypeORM em Typescript

Suponha que desejamos criar uma entidade `Usuario` usando o TypeORM:

```typescript
import { Entity, PrimaryGeneratedColumn, Column } from "typeorm";

@Entity()
class Usuario {
    @PrimaryGeneratedColumn()
    id: number;

    @Column()
    nome: string;

    @Column()
    email: string;

    @Column()
    senha: string;

    // Outros campos e métodos da entidade Usuario
}

// Exemplo de uso:
const novoUsuario = new Usuario();
novoUsuario.nome = "Alice";
novoUsuario.email = "alice@example.com";
novoUsuario.senha = "senha_segura";

// Agora você pode persistir esse usuário no banco de dados usando o TypeORM
```


- `@Entity()`: Marca a classe `Usuario` como uma entidade do banco de dados.
- `@PrimaryGeneratedColumn()`: Define a coluna `id` como uma chave primária gerada automaticamente.
- `@Column()`: Mapeia as propriedades `nome`, `email` e `senha` para colunas na tabela do banco de dados. 