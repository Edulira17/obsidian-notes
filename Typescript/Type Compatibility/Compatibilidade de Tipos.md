
É o mecanismo usado pelo TypeScript para verificar se um tipo pode ser atribuído a outro. Essa compatibilidade é **estrutural**, ou seja, baseada na forma ou estrutura de um tipo, em vez de depender explicitamente de hierarquias de classes ou interfaces.

### **Como Funciona a Compatibilidade de Tipos?**

O TypeScript verifica se um tipo é compatível comparando suas propriedades. Se o objeto ou tipo que você está atribuindo possui pelo menos as propriedades requeridas pelo tipo-alvo, ele será considerado compatível.

**Exemplo de Compatibilidade Estrutural**:

``` typescript
interface Pessoa {
  nome: string;
  idade: number;
}

const usuario = { nome: "Eduardo", idade: 20, ativo: true };

const pessoa: Pessoa = usuario; // OK, porque `usuario` tem as propriedades necessárias de `Pessoa`
```

Mesmo que `usuario` tenha uma propriedade extra (`ativo`), ele ainda é compatível com o tipo `Pessoa`, pois `Pessoa` exige apenas `nome` e `idade`.