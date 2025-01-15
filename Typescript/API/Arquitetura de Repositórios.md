
A arquitetura de repositórios ==é um padrão de projeto comum no desenvolvimento de software que ajuda a separar a lógica de acesso a dados da lógica de negócios.== Ela é frequentemente usada em aplicativos que precisam interagir com bancos de dados, sistemas de arquivos ou fontes de dados externas. Vamos explorar o que é a arquitetura de repositórios, porque ela é importante e como ela pode ser implementada.

![[repository.webp]]

Ela introduz uma abstração chamada **repositório** que atua como uma interface entre o código, que precisa acessar dados, e a fonte real dos dados, seja um banco, um serviço da web ou outro sistema de armazenamento.

Imagine um contrato que define de que forma um serviço de armazenamento de usuários deve funcionar. Nele temos acordos sobre o que podemos fazer com os usuários, como adicionar, obter, atualizar e excluir. Esse contrato é normalmente implementado como uma **interface**:

```typescript
interface RepositorioDeUsuarios {
    adicionarUsuario(usuario: Usuario): void;
    obterUsuarioPorId(id: number): Usuario | undefined;
    atualizarUsuario(usuario: Usuario): void;
    excluirUsuario(id: number): void;
}
```


Agora, imagine que temos uma classe que “assina o contrato”, fazendo a implementação dele e fornecendo detalhes sobre como interagir com os usuários.

```typescript
class RepositorioDeUsuarios implements RepositorioDeUsuarios{
    private usuarios: Usuario[] = [];

    adicionarUsuario(usuario: Usuario): void {
        this.usuarios.push(usuario);
    }

    obterUsuarioPorId(id: number): Usuario | undefined {
        return this.usuarios.find(user => user.id === id);
    }

    atualizarUsuario(usuario: Usuario): void {
        const index = this.usuarios.findIndex(user => user.id === usuario.id);
        if (index !== -1) {
            this.usuarios[index] = usuario;
        }
    }

    excluirUsuario(id: number): void {
        this.usuarios = this.usuarios.filter(user => user.id !== id);
    }
}
```

Assim como um contrato define as regras e expectativas, a interface de repositório define as operações possíveis e as expectativas de comportamento.

A forma com que esses métodos serão implementados (com Postgres, SQLite, MongoDB, local, etc) não depende de um controller ou de outra camada. Podemos ter vários repositórios e decidir qual usar no controller posteriormente. Da mesma forma que um contrato pode ser assinado por diferentes partes, a interface de repositório pode ser implementada por diferentes classes, desde que cumpram o contrato.

O nosso controller não deve se preocupar com a maneira como isso é implementado, ele apenas contratou um conjunto de serviços para adicionar, obter, atualizar e excluir um usuário.

Ainda pensando na analogia de um contrato, mudanças nos termos de um contrato podem ser feitas sem afetar a outra parte, semelhantemente, alterações na interface de repositório podem ser feitas sem modificar o código que a utiliza.

## Vantagens da arquitetura de repositórios

A arquitetura de repositórios oferece várias vantagens:

1. **Abstração de dados:** Ela fornece uma camada de abstração que permite que o código de negócios trabalhe com dados de forma genérica, sem se preocupar com os detalhes da fonte de dados real.
    
2. **Testabilidade:** ela facilita a criação de testes unitários, pois você pode criar implementações de repositórios falsas ou de teste que não dependem de uma fonte de dados real.
    
3. **Flexibilidade:** permite que você mude a fonte de dados subjacente (por exemplo, de um banco de dados relacional para um banco de dados NoSQL) sem alterar o código de negócios.
    

A implementação da arquitetura de repositórios envolve os seguintes componentes:

1. **Interface de repositório:** defina uma interface que descreva as operações que a camada de negócios pode realizar no repositório. Por exemplo, métodos para criar, ler, atualizar e excluir dados.
    
2. **Classe de repositório concreta:** crie uma classe que implemente a interface de repositório. Essa classe interage diretamente com a fonte de dados real (por exemplo, um banco de dados) e executa as operações específicas da fonte de dados.
    
3. **Camada de negócios:** a camada de negócios usa a interface de repositório para interagir com os dados, sem se preocupar com os detalhes da implementação do repositório.
    

Em resumo, a arquitetura de repositórios é uma abordagem eficaz para organizar e abstrair o acesso a dados em um aplicativo, tornando-o mais flexível, testável e fácil de manter.

É especialmente útil quando você precisa lidar com várias fontes de dados ou deseja isolar a lógica de negócios do acesso direto aos dados.