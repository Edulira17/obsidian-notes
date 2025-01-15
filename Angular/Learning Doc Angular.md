.326
## Updating the Component Class

No Angular, a lógica e o comportamento do componente são definidos na classe TypeScript do componente.

Neste exemplo, você aprenderá como atualizar a classe do componente e como usar a interpolação.

``` typescript
export class AppComponent {
  city = 'San Francisco';
}
```

A propriedade city é do tipo string, mas você pode omitir o tipo por causa da inferência de tipo no TypeScript. A propriedade city pode ser usada na classe AppComponent e pode ser referenciada no template do componente.

Para usar uma propriedade de classe em um modelo, você precisa usar a sintaxe `{{ }}`.

**Update the component template**

``` typescript
template: `Hello {{ city }}`,
```

Este é um exemplo de interpolação e é parte da sintaxe de template do Angular. Ele permite que você faça muito mais do que colocar texto dinâmico em um template. Você também pode usar essa sintaxe para chamar funções, escrever expressões e muito mais.


## Composing Components

A propriedade `selector` da configuração do componente fornece um nome para usar ao referenciar o componente em outro template. Você usa o seletor como uma tag HTML, por exemplo `app-user` seria `<app-user />` no template.

``` typescript
template: `<app-user />`,
imports: [UserComponent]
```

O componente agora exibe a mensagem Username: youngTech. Você pode atualizar o código do modelo para incluir mais marcação.

Como você pode usar qualquer marcação HTML que quiser em um modelo, tente atualizar o modelo para AppComponent para também incluir mais elementos HTML. Este exemplo adicionará um elemento `section` como pai do elemento `app-user` 

``` typescript
template: `<section> <app-user /> </section>`,
```


## Control Flow in Components - @if

Para expressar exibições condicionais em modelos, o Angular usa a sintaxe de modelo `@if`.

Aqui está um exemplo de como usar a sintaxe @if em um componente:

``` typescript
@Component({
  ...
  template: `
    @if (isLoggedIn) {
      <p>Welcome back, Friend!</p>
    }
  `,
})
class AppComponent {
  isLoggedIn = true;
}
```

==OBS:== 

1. Há um prefixo `@` para if porque é um tipo especial de sintaxe chamado sintaxe de modelo Angular.
2. Para aplicativos que usam v16 e anteriores, consulte a documentação Angular para NgIf para obter mais informações.


**Exemplo:**
``` typescript
import {Component} from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <span>
      @if(isServerRunning) {
        <p>O servidor está funcionando</p>
      }@else {
        <p>Erro ao se conectar no servidor</p>
      }
    </span>
  `,
})
export class AppComponent {
  // add the boolean property here
  isServerRunning: boolean = false
}
```



## Control Flow in Components - @for

Muitas vezes, ao criar aplicativos da web, você precisa repetir algum código um número específico de vezes. Por exemplo, dado um conjunto de nomes, você pode querer exibir cada nome em uma tag `<p>`.

A sintaxe que permite repetir elementos em um modelo é @for: 

``` typescript
@Component({
  ...
  template: `
    @for (os of operatingSystems; track os.id) {
      {{ os.name }}
    }
  `,
})
export class AppComponent {
  operatingSystems = [{id: 'win', name: 'Windows'}, {id: 'osx', name: 'MacOS'}, {id: 'linux', name: 'Linux'}];
}
```


## Property Binding in Angular

A vinculação de propriedades no Angular permite que você defina valores para propriedades de elementos HTML, componentes Angular e muito mais.


