# Angular

### Menu

- [1 - Básico](#1-básico)
   - [1.1 - Componente](#11-componente)
   - [1.2 - Módulo](#12-módulo)
   - [1.3 - Comparação entre módulos e componentes](#13-comparação-entre-módulos-e-componentes)
   - [1.4 - Regras](#14-regras)
   - [1.5 - Elementos HTML](#15-elementos-html)
     - [1.5.1 - Atributos](#151-atributos)
     - [1.5.2 - Propriedades](#152-propriedades)
     - [1.5.3 - Resumo](#153-resumo)

- [2 - Utilizando o Angular - O Básico](#2-utilizando-o-angular---o-básico)
   - [2.1 - Property Binding](#21-property-binding)
   - [2.2 - Event Binding](#22-event-binding)
   - [2.3 - Attribute Binding](#23-attribute-binding)
   - [2.4 - Style Binding](#24-style-binding)
   - [2.5 - Class Binding](#25-class-binding)

- [3 - Decorators Mais Comuns](#3-decorators-mais-comuns)
   - [3.1 - @Input()](#31-decorator-input)
     - [3.1.1 - Input('\<ALIAS\>')](#311-inputalias)
     - [3.1.2 - Input({required:true})](#312-inputrequiredtrue)
     - [3.1.3 - Input({required: \<boolean\>, alias: \<string\>, transform: \<function\>})](#313-inputrequired-boolean-alias-string-transform-function)
     - [3.1.4 - Input com get e set](#314-input-com-get-e-set)
   - [3.2 - @Output()](#32-decorator-output)
     - [3.2.1 - Output('<ALIAS>')](#321-outputalias)
   - [3.3 - Two-Way-Data-Binding](#33-two-way-data-binding)

- [4 - Diretivas Mais Comuns](#4-diretivas-mais-comuns)
   - [4.1 - Diretiva *ngIf](#41-diretiva-ngif)
   - [4.2 - Diretiva *ngFor](#42-diretiva-ngfor)
   - [4.3 - Diretiva de atributo NgStyle](#43-diretiva-de-atributo-ngstyle)
   - [4.4 - Diretiva de atributo NgClass](#44-diretiva-de-atributo-ngclass)
   - [4.5 - Introdução aos Pipes](#45-introducao-aos-pipes)


- [5 - Escopos, Template Variables e Diretivas](#5-escopos-template-variables-e-diretivas)
   - [5.1 - Escopos](#51-escopos)
   - [5.2 - Template Variables](#52-template-variables)
     - [5.2.1 - Como Utilizar Diretamente no HTML](#521-como-utilizar-diretamente-no-html)
     - [5.2.2 - Como Utilizar no Typescript](#522-como-utilizar-no-typescript)
     - [5.2.3 - Como Utilizar @ViewChild](#523-como-utilizar-com-viewchild)
     - [5.2.4 - Acessando Atributos e Métodos do Componente Referenciado](#524-acessando-atributos-e-métodos-do-componente-referenciado)
     - [5.2.5 - Acessar Child na Renderização do Componente](#525-acessar-child-na-renderização-do-componente)
     - [5.2.6 - Usando @ViewChildren()](#526-usando-viewchildren)
     - [5.2.7 - ElementRef](#527-elementref)
   - [5.3 - Diretivas](#53-diretivas)
     - [5.3.1 - Como Criar Diretiva de Atributo](#532-como-criar-diretiva-de-atributo)
     - [5.3.2 - Como Passar Valores para as Diretivas](#533-como-passar-valores-para-as-diretivas)



-----
# 1. Básico

## 1.1. Componente:

### **O que é?**

- Uma lógica que deve ser reutilizada em outros locais diferentes.
- Pode receber variáveis.

### **Propriedades dos componentes:**

```
    @Component({
      selector: 'app-<NAME>',
      templateUrl: './<NAME>.component.html',
      styleUrl: './<NAME>.component.scss',
    })
    export class <NAME>Component {
      // CODIGO DO COMPONENTE
    }
```

- selector: é o nome da tag para chamar o componente;
- templateUrl: é o caminho para o HTML do componente;
- template: é o HTML de modo inline dentro do arquivo .ts;
  - OBS.: caso seja utilizado o template, não deve ser utilizado o templateUrl
- styleUrl: é o caminho para o CSS, SCSS, etc. do componente;
- stylesUrl: é um array de caminhos para styles do componente;
- styles: é um arquivo de styles inline dentro do .ts;
  - OBS.: caso seja utilizado o styles, pode ser utilizado o stylesUrl ou o StyleUrl junto,
  o angular irá mesclar os dois, dando prioridade à:
    1. <style></style> dentro de template ou templateUrl;
    2. styles: ``;
    3. stylesUrl: ['segundo.scss', 'primeiro.scss'];
- encapsulation: encapsula o SCSS. Por default, ele afeta somente o do próprio componente.
  - viewEncapsulation.none: o SCSS do componente vira global (altera outros componentes);
  - viewEncapsulation.emulated: o SCSS do componente altera somente o proprio componente. É a configuração DEFAULT;
  - viewEncapsulation.shadowDom: o SCSS do componente altera somente o proprio componente e nada pode afetar o proprio componente,
  apenas pode afetar os componentes filhos.

## 1.2. Módulo:

### **O que é?**

- Utilizado para organizar componentes que tem lógicas similares.

### **Propriedades dos módulos:**

```
    @NgModule({
      declarations: [
        AQUI VEM AS DECLARAÇOES DOS COMPONENTES DO MÓDULO
      ],
      imports: [
        AQUI VEM AS IMPORTAÇOES DOS MÓDULOS PARA USAR
        OS COMPONENTES DELES
      ],
      providers: [],
      bootstrap: [
        UTILIZADO PARA INICIALIZAR A APLICAÇAO (UTILIZADO
        NORMALMENTE APENAS COM O APP.MODULE.TS
      ]
    })
    export class <MODULE_NAME>Module { }
```

## 1.3. Comparação entre módulos e componentes:

*Uma estante de livros*

- A estante é a aplicação
- As divisões de seções são os módulos (ex.: terror, suspense, ...)
- Os livros são os componentes
  - Livros de terror devem estar na seçao de terror, etc...

## 1.4. Regras:

- Componentes só podem ser declarados em um módulo. Para utilizar em outro módulo:
  - Exportar o componente no seu módulo.
  - No módulo onde deseja usar o componente, importar o **MODULO** do componente.
    - Modulos sempre se importam!
  - Desse modo, tudo que for exportado no módulo importado, pode ser usado no outro módulo.

## 1.5. Elementos HTML:

### 1.5.1 Atributos

- Setados no HTML, como, por exemplo, class, id, ...
- Tem 2 tipos, e cada elemento pode ou nao ter os dois, depende do elemento:
  - Atributos globais: class, id, etc...
  - Atributos de eventos: onclick, onmouseover, etc...

### 1.5.2 Propriedades

- Quando a página é renderizada, é gerada uma árvore de propriedades pelo DOM.
- Essa arvore de propriedades torna os elementos configuraveis pelo DOM através
de javascript/typescript.
- Exemplos: elemento.value, elemento.defaultValue, elemento.tagName, etc...

### 1.5.3 Resumo:

- Atributos são alterados diretamente no HTML.
- Propriedades são alteradas via javascript/typescript, e cada elemento possui um objeto
de propriedades para ser acessado, criado no momento da renderização do elemento.

-----

# 2. Utilizando o Angular - ***O básico***

## 2.1 Property Binding

### **[Property]="variable"**

- Atribui a variável com a propriedade (direita para esquerda).
- É passado o valor da variável para a propriedade e renderizado o elemento.
- **Não passa o valor da propriedade para a variável!!!**

## 2.2 Event Binding

### **(Event)="function()" // (Event)="function($event)**

- Atribui o evento a uma função (esquerda para direita).
- É passada uma função que vai ser executada quando o evento acontecer.

## 2.3 Attribute Binding

### ***[attr.atribute]="variable"***

- Atribui a variável com o atributo (direita para esquerda).
- É passado o valor da variável para o atributo diretamente.

## 2.4 Style Binding

### **[style.\<STYLENAME\>]="Variavel" (*variavel tem que ser string*)**

- Adiciona um Style \<STYLENAME\> CSS do componente (como se fosse adicionar ao atributo style)
- É passado o valor da variável para a propriedade style dinamicamente

## 2.5 Class Binding

### **[class.\<CLASSNAME\>]="Variavel" (*variavel tem que ser boolean*)**

- Adiciona uma classe \<CLASSNAME\> ao componente (como se fosse adicionar ao atributo class)
- É passada a classe ao lado de class., caso a variavel seja 'true',
a classe é renderizada.

### **[class]="Variavel" (*variavel tem que ser string*)**

- É passada a classe na variável, podendo ser uma ou mais classes.

### **[class]="{ '\<CLASSNAME\>' : variavel }" (*variavel tem que ser boolean*)**

- É passado um objeto com classes, sendo a key o nome da classe \<CLASSNAME\> e seu valor
um boolean para informar se ela é true ou false.

-----

# 3. Decorators Mais Comuns

## 3.1 Decorator @Input()

- Recebe os dados do componente pai através de Property Binding
  - Ex.:

```
(child.component.ts)

  @Input() original: type = value;

(parent.component.html)

  <component
    [original]="newValue"
  ></component>
```

### 3.1.1 Input('\<ALIAS\>')

- O valor de \<ALIAS\> é o nome da propriedade que vai ser usada para o Binding
  - Ex.:

```
(child.component.ts)

  @Input('alias') original: type = value;

(parent.component.html)

  <component
    [alias]="newValue"
  ></component>
```

### 3.1.2 Input({required:true})

- Passando um objeto com required:true, faz com que o input seja obigado a ser
preenchido quando o componente for chamado.
- Gera um erro em tempo de compilação, ou seja, não gera erro em tempo de execução.
  - Ex.:

```
(child.component.ts)

  @Input({required:true}) original: type = value;

(parent.component.html)

  // Caso não seja definido um valor para o input [original]
  // um erro na compilação irá ocorrer.

  <component
    [original]="newValue"   
  ></component>
```

### 3.1.3 Input({required: \<boolean\>, alias: \<string\>, transform: \<function\>})

- Required = Faz com que o Binding seja obrigatorio;
- Alias = Cria um alias para a propriedade;
- Transform = Recebe uma função que irá retornar um valor do mesmo tipo do Input, podendo
  transformar o valor recebido, como, por exemplo, retirar espaços, etc.
  - Ex.:

```
(child.component.ts)

  @Input({
    required:true,
    alias: 'alias',
    transform: (value) => {transformedValue},
  }) original: type = value;

(parent.component.html)

  <component
    [alias]="newValue"   
  ></component>
```

### 3.1.4 Input com get e set

- Usar get e set para receber um input pode ser útil caso seja necessário 'modificar'
  o input antes de salvá-lo ou mesmo mostrá-lo.
- Pode ser alterado no setter, alterando o valor salvo, ou alterado no getter, alterando
  apenas o valor mostrado. (Ou em ambos)
  - Ex.:

```
  private _variable: string = '';

  @Input() set variable(value: type){
      // Faz a transformação do valor recebido com value
      this._variable = value;
    }
    get variable(){
      // Retorna o valor para ser utilizado
      return this._variable;
    }
```

## 3.2 Decorator @Output()

- Envia dados do componente filho para o componente pai
  - Ex.:

```
(child.component.ts)

  // Define qual será o nome do output e qual tipo de evento vai emitir
  @Output() outputName = new EventEmmiter<emitType>()
  
  // Define uma função para emitir o evento
  functionChildName(){ this.outputName.emit(value: emitType) }
  
(child.component.html)

  // Define uma ação para disparar a função que emite o evento
  <div (click)="functionChildName()"><div>
  
(parent.component.html)

  // Recebe o evento com seu valor dentro de uma função a ser
  // usada dentro do componente pai
  <child (outputName)="functionParentName($event)"></child>
  
(parent.component.ts)

  // Faz algo com o evento recebido (evento terá o mesmo valor do enviado no filho)
  functionParentName(event: emitType){
    console.log(event);
  }

// OBS.:
// - Não é obrigatório passar um valor no evento, pode ser apenas uma ação
//   como por exemplo o click de um botão retornando void, que apenas irá
//   disparar uma função no componente pai.
// - Sempre que for passado um valor para o evento, deve ser passado na função
//   estritamente como $event, caso contrário, ocorrerão erros.
```

### 3.2.1 Output('\<ALIAS\>')

- Passa um \<ALIAS\> para o Output. (*funciona do mesmo modo que para o input*)

## 3.3 Two-Way-Data-Binding

- Sincroniza dois valores, mesclando Input() e Output() simultaneamente.
  - Ex.:

```
(component.html)
 
  <input type="text" [(ngModel)]="name" />
  <span> Nome digitado: {{ name }} </span>
 
(component.ts)

  public name: string = 'valor';
```

- [ngModel]="name"  ***(Input)***
- (ngModelChange)="handleName($event)"  ***(Output)***
- [(ngModel)]="name" ***(Input e Output)***
  - Todos métodos podem ser usados juntos!
  - Caso o output altere a variável e seja utilizado junto com ngModel,
    a prioridade é para a atribuição do **OUTPUT**!!

-----

# 4. Diretivas Mais Comuns

## 4.1 Diretiva *ngIf

- Realiza a renderização do elemento onde a diretiva está conforme o resultado.
- Caso seja false, nao renderiza o componente no DOM.
- Caso seja true, renderiza o componente no DOM.
- O Angular fica sempre verificando esse valor, sendo possível tornar um elemento
  visivel/invisível dinamicamente.
  - Ex.:

```
  <div *ngIf="false">Não apareço no DOM</div>
  <div *ngIf="{}">Não apareço no DOM</div>
  <div *ngIf="[]">Não apareço no DOM</div>
  <div *ngIf="''">Não apareço no DOM</div>
  <div *ngIf="null">Não apareço no DOM</div>
  <div *ngIf="undefined">Não apareço no DOM</div>
  <div *ngIf="NaN">Não apareço no DOM</div>
  <div *ngIf="true">Apareço no DOM</div>
  <div *ngIf="{<objetos não vazios>}">Apareço no DOM</div>
  <div *ngIf="[<arrays não vazios>]">Apareço no DOM</div>
  <div *ngIf="'<strings não vazias'">Apareço no DOM</div>
```

- Para realizar um 'else', podemos usar o **ng-template**
- Podemos também usar o then-else com **ng-container** e **ng-template**
- Ex.:

```
  // APENAS ELSE
  
  <div *ngIf="false; else elseTemplate"> SOU O IF </div>
  <ng-template #elseTemplate> // essa tag nâo é renderizada, somente o que está dentro
    <div>SOU O ELSE</div>
  </ng-template>
  
  // IF E ELSE SEPARADOS EM DOIS TEMPLATES
  
  <ng-container *ngIf="false; then trueTemplate; else falseTemplate"></ng-container>
  <ng-template #trueTemplate>
    <div>True Template</div>
  </ng-template>
  <ng-template #falseTemplate>
    <div>False Template</div>
  </ng-template>
```

## 4.2 Diretiva *ngFor

- Realiza uma renderização com um laço 'for' em um componente, baseado em dados.
  - Ex.:

```
(component.html)
  
  <div class="list">
    <div class="item" *ngFor="let person of listPeople">
      <p class="item__name">{{person.name}}</p>
      <p class="item__age">{{person.age}}</p>
    </div>
  </div>

(component.ts)

  listPeople = [
    {name: 'Felipe', age: 25},
    {name: 'Maria', age: 22},
    {name: 'Pedro', age: 23},
    {name: 'Antonio', age: 24},
  ];
```

### **Mais Comum de ser utilizado**

- *ngFor="let item of items; let i of index"
  - item é o valor iteravel dentro de items
  - i é o indice do array/objeto percorrido
  - **i tem que apontar sempre para INDEX** *(não pode ser outro nome)*

### **Outras props:**

```
  <div *ngIf="listPeople" class="list">
    <div class="item"
         [class.item--odd]="isOdd"
         [class.item--highlighted]="isEven"
         *ngFor="
         let person of listPeople;  // valor iteravel
         let i = index;             // index do array/objeto
         let isOdd = odd;           // retorna true se for impar
         let isEven = even;         // retorna true se for par
         let isFirst = first;       // retorna true se for o primeiro valor
         let isLast = last;         // retorna true se for o último
    ">
      <p *ngIf="isFirst" class="item__name">É o primeiro</p> 
      //será renderizado só no primeiro
      <p class="item__name">{{ i }} - {{person.name}}</p>
      <p class="item__age">{{person.age}}</p>
      <p *ngIf="isLast" class="item__name">É o último</p> 
      //será renderizado só no último
    </div>
  </div>

```

## 4.3 Diretiva de atributo NgStyle

- Deixa as propriedades passadas para ele de forma dinâmica.
- O angular fica monitorando por mudanças de atributo para renderizar em tempo de execução.
  - Ex.:

```
(component.html)
  
  <h1 [ngStyle]="{
    'font-size': fontSize + 'px',
    'color': textColor,
  }">
    TEXTO COM STYLES DINAMICOS
  </h1>

(component.ts)

  // Se esses atributos forem mudados em tempo de execução, o angular atualizara quase instantaneamente
  // como estilos do elemento
  
  fontSize: number = 15;
  textColor: 'white' | 'orange' = 'white'
```

## 4.4 Diretiva de atributo NgClass

- Deixa as classes passadas atuando de forma dinâmica.
- O angular fica monitorando por mudanças de classes para renderizar em tempo de execução.
- Pode receber um objeto relacionando classes com booleanos (true ou false para definir se serão renderizadas)
- Pode receber uma string de classes, separadas por um espaço ('class1 class2 class3')
- Pode receber um array de classes (['classe1', 'classe2', 'classe3'])
- Pode receber um objeto de classes com booleanos ({'class1 class2' : true, 'class3' : true, 'class4' : false})
  - Ex.:

```
(component.html)
  
  <h1 [ngClass]="{
    'is-green': isGreen',
    'is-white': !isGreen,
  }">
    TEXTO COM CLASSE DINAMICA
  </h1>

(component.ts)
  
  // Se esses atributos forem mudados em tempo de execução, o angular atualizara quase instantaneamente
  // como classe do elemento
  
  isGreen: boolean = false;
  toogleColor(){
    this.isGreen = !this.isGreen;
  }

(component.scss)
  
  .is-white{
    color = white;
  }
  
  .is-green{
    color = green;
  }
```

## 4.5 Introdução aos Pipes

### **Para que servem e como usar:**

- Transformam um valor eemm outro valor, reduzindo a logica dentro do template e atribuindo
  ao pipe.
- O angular fornece alguns pipes, como, por exemplo, 'uppercase', que transforma o texto
  para uppercase, 'json', que mostra um objeto sem precisar iterar sobre ele, ...
  - Ex.:

```
(component.html)

  <h1>{{ text | uppercase }}</h1>
  // Resultado será TEXTO
  
  <h1>{{ object | json }}</h1>
  // Resultado será { "name": "Nome", "age": 25 }
  // Sem a pipe seria [Object object]

(component.ts)

  text: string = 'texto';
  object = {
    name: 'Nome',
    age: 25
  };
```

### **Como criar um Pipe:**

- A Pipe é uma classe e terá um decorator @Pipe({...}) para identificar ela.
- Dentro do decorator, terá uma configuração de 'name', que é o nome que
  será usado para usar a pipe no código. O nome deve fazer sentido e ser parecido
  com o nome da classe.
- Ela implementará a classe PipeTransform, que implementa o método 'transform'.
- O método transform recebe valor/valores e retorna valor/valores.
- Deve ser importado no módulo onde vai ser usado, ou tornado standalone para
  ser importado nos componentes diretamente.
  - Ex.:

```
(status-class.pipe.ts)
  
    import {Pipe, PipeTransform} from "@angular/core";
    
    @Pipe({
      name: 'statusClass'
    })
    export class StatusClassPipe implements PipeTransform{
      transform(status: number): string {
        const obj: {[key:number] : string} = {
          1: 'active',
          2: 'partial',
          3: 'blocked'
        };
        return obj[status];
      }
    }

(component.ts)
  
  pessoa1 = {
    nome: 'Lucas',
    status: 1
  };
  pessoa2 = {
    nome: 'Joao',
    status: 2
  }
  pessoa3 = {
    nome: 'Maria',
    status: 3
  }

(component.scss)

  body{
    color: white;
  }
  .active{
    background-color: green;
  }
  .partial{
    background-color: orange;
  }
  .blocked{
    background-color: red;
  }

(component.html)
  
  <h1 [class]="pessoa1.status | statusClass">{{ pessoa1.nome }}</h1> //Aplicada .active
  <h1 [class]="pessoa2.status | statusClass">{{ pessoa2.nome }}</h1> //Aplicada .partial
  <h1 [class]="pessoa3.status | statusClass">{{ pessoa3.nome }}</h1> //Aplicada .blocked
```

-----

# 5 Escopos, Template Variables e Diretivas

## 5.1 Escopos

### **Como funciona:**

- Um componente pai nao consegue acessar variaveis do escopo do componente filho;
- Um componente filho consegue acessar variaveis do escopo do componente pai;
- Ex. com funções em JS:

```
    const funcaoPai = () => {
        let pai = 'pai';
        
        // IRA DAR ERRO, POIS O CONTEUDO DA FILHA NÃo ESTÁ
        // ACESSÍVEL PARA O PAI
        console.log(filha); 
        
        const funcaoFilha = () => {
            let filha = 'filha';
            
            // NÃO IRA DAR ERRO, POIS O CONTEUDO DE PAI ESTÁ
            // ACESSÍVEL PARA A FILHA
            console.log(pai);
        }
    }
```

- Ex. com template variables:

```
    <div class="primo">
        // ESSA DECLARAÇÃO RESULTARA EM ERRO, POIS O inputPai 
        // NAO ESTÁ ACESSÍVEL NESSE ESCOPO
        {{ inputPai }}
    </div>

// QUANDO TEMOS UM *ngIf OU UM *ngFor, OU ALGUMA DIRETIVA,
// CRIAMOS UM ESCOPO NO COMPONENTE, FAZENDO COM QUE O QUE FOR
// REFERENCIADO DENTRO DELE NÃO SEJA ACESSÍVEL FORA

    <div class="pai" *ngIf="true">
        // ESSE TEMPLATE VARIABLE SÓ VAI SER ACESSÍVEL DENTRO
        // DO COMPONENTE PAI
        <input #inputPai>
        
        // ESSA DECLARAÇÃO RESULTARA EM ERRO, POIS O inputFilha 
        // NAO ESTÁ ACESSÍVEL NESSE ESCOPO
        {{ inputFilha }}
        
        <div class="filha" *ngIF="true">
            // ESSE TEMPLATE VARIABLE SÓ VAI SER ACESSÍVEL DENTRO
            // DO COMPONENTE FILHA
            <input #inputFilha>
            
            // ACESSÍVEL EM FILHA
            {{ inputPai }}
        
        </div>
    </div>
```

## 5.2 Template Variables

### **Para que serve:**

- Ter acesso a propriedades de um componente filho de forma dinâmica.

### 5.2.1 Como utilizar: ***(diretamente no HTML)***

- Usar o #\<NOME\> referencia o elemento a ser acessado;
- Usar o ngModel faz com que o Angular ative o changeDetection para o elemento,
  escutando as mudanças do elemento em tempo de execução;
- As propriedades podem ser acessadas através do uso de \<NOME\> referenciado
  no componente, seguido pela propriedade a ser acessada.
- Ex.: 

```
(component.html)

    <input type="text" #meuInput ngModel />
    <span> Valor: {{ meuInput.valor }} </span>
    
(module.ts)

    import {FormsModule} from "@angular/forms";
    
    @NgModule({
        imports: [
            FormsModule
        ]
    })
    export class Module{ }
```

### 5.2.2 Como utilizar: ***(no Typescript)***

- As definições do componente no HTML serão iguais;
- No arquivo .ts podemos receber esse elemento através de uma função
  que retorne o proprio elemento, assim, temos acesso a ele dentro do
  arquivo para manipulações das propriedades.
- Ex.:

```
(component.html)

    <input type="text" #meuInput ngModel />
    <span> Valor: {{ meuInput.valor }} </span>
    <button (click)="onClick(meuInput)"> Receber Valor </button>
    
(component.ts)

    clicou(meuInput: HTMLInputElement){
    
        // PODEMOS ACESSAR AS PROPRIEDADES
        console.log(meuInput.value);
        
        // PODEMOS TAMBEM ALTERAR AS PROPRIEDADES
        meuInput.value = 'Novo texto';
    }
```

### 5.2.3 Como utilizar @ViewChild

- As definições do componente no HTML serão iguais;
- No arquivo .ts recebemos o template variable dentro do @ViewChild('\<NOME\>');
- Apos definir a ViewChild, definimos como iremos chamá-la no .ts e sua tipagem.
- Ex.:

```
(component.html)

    <input type="text" #meuInput>
    
    <button (click)="updateInputText()">Atualizar</button>
    
(component.ts)

    @ViewChild('meuInput') meuInputElement!: ElementRef<HTMLInputElement>;
    
    updateInputText(){
        this.meuInputElement.nativeElement.value = 'Novo texto!';
    }
```

### 5.2.4 Como acessar atributos e métodos do componente referenciado:

- Com @ViewChild() podemos acessar os métodos e alterar os atributos de um componente.
- Ex.:

```
(filho.ts)

  public attribute: string = 'some value';
  public method(value: string) {
    console.log(value);
  }
  
(pai.html)

  <filho #filhoRef></filho>
  
(pai.ts)

  @ViewChild('filhoRef') filho!: FilhoComponent;

  // METODO DO PAI QUE QUANDO ATIVADO IRÁ ACIONAR UMA
  // FUNÇÃO CRIADA NO FILHO, QUE IRÁ ACESSAR UM
  // ATRIBUTO CRIADO NO FILHO
  
  altFilhoMethod(){
    this.filho.method( this.filho.attribute );
  }
```

### 5.2.5 Acessar child na renderização do componente:

- Caso tentamos acessar o componente com @ViewChild no constructor da classe,
  ou até mesmo no ngOnInit, teremos um erro, pois nessas etapas do componente,
  os binds ainda não foram resolvidos.
- Para resolver esse problema, devemos utilizar o ***ngAfterViewInit***, que irá executar
  a view após os binds estarem resolvidos, sem gerar erros.
- Ex.:

```
(component.html)

  Meu Input:
    <input
      type="text"
      *ngIf="true"
      #meuInput>

(component.ts)

  @ViewChild('meuInput') meuInput!: ElementRef<HTMLInputElement>;

  constructor() { // Executa primeiro
  }

  ngOnInit() { // Executa após o contructor
   
    // Daria erro pois o componente nao foi renderizado ainda.
    this.meuInput.nativeElement.focus();

  }

  // Executa após todos binds serem resolvidos
  
  ngAfterViewInit() { // Executa após o ngOnInit

    this.meuInput.nativeElement.focus();

  }
```

### 5.2.6 Usando @ViewChildren()

- Usamos o @ViewChildren para referenciar varios elementos de uma única vez
  em um template.
- Podemos controlar individualmente cada componente, ou controlar todos ao mesmo tempo.
- Podemos alterar propriedades, verificar se alguma children foi excluida/incluida, ...
- Ex.:

```
(componente.html)

  <button #meuButton 
    class="btn-{{ i }}" 
    *ngFor="let btn of buttonsList; let i = index"
    (click)="changeColor($event)"
  >
    {{btn}}  
  </button>

  <button (click)="resetButtons()">
    Resetar
  </button>

  <button (click)="first()">
    Pegar Primeiro
  </button>

  <button (click)="remove()">
    Remover Item
  </button>


(componente.ts)

  // Uma lista para gerar dinamicamente botões
  
  buttonsList = [
    'Botao 1',
    'Botao 2',
    'Botao 3',
  ];

  // Declaração dos botões dentro do ViewChildren
  // As declarações de viewChildren serão sempre do tipo QueryList
  // A tipagem do QueryList será do tipo dos elementos children
  
  @ViewChildren('meuButton') buttonsEl!: QueryList<ElementRef<HTMLButtonElement>>

  // Com a estrutura do ngAfterViewInit podemos fazer manipulações de forma
  // correta ao inicializar o componente
  
  ngAfterViewInit() {
  
    console.log(this.buttonsEl);

    // Quando muda a estrutura do ViewChildren, atualiza os valores
    // OBS.: APENAS A ESTRUTURA, NÃO OS ATRIBUTOS E MÉTODOS DOS
    // ELEMENTOS CHILDREN
    
    this.buttonsEl.changes.subscribe(result => {
      console.log(result);
    })
  }

  // Podemos ter funções que recebem o elemento referenciado no $event
  // podendo assim, alterar um por vez quando algo relacionado ao elemento
  // ocorrer, podendo alterar suas propriedades
  
  changeColor(event: Event){
    const btnElement = event.target as HTMLButtonElement;
    btnElement.style.backgroundColor = 'Orange';
    btnElement.style.color = 'white';
  }

  // Podemos fazer um forEach, selecionando todos elementos e definindo
  // um comportamento ou mudança de propriedades à eles
  
  resetButtons() {
    this.buttonsEl.forEach(button => {
      button.nativeElement.style.color = 'black';
      button.nativeElement.style.backgroundColor = '';
    })
  }
  
  // Podemos selecionar apenas um elemento de várias formas,
  // como um nome de classe, sua posição dentro do array de
  // children, sua posição dentro da QueryList, etc...

  first(){

    // pegar com referencia a ordenação

    const primeiro = this.buttonsEl.get(0);
    console.log(primeiro);

    // pegar com referência a classe

    const primeiro = this.buttonsEl.find((btn) => (
      btn.nativeElement.className === 'btn-0'
    ));
    console.log(primeiro);

    // pegar com referencia ao array

    const primeiro = this.buttonsEl.toArray()[0];
    console.log(primeiro)
    
  }

  // Método que altera a estrutura dos elementos da
  // @ViewChildren, ativando o método change da mesma
  
  remove(){
    this.buttonsList.shift();
  }
```

### 5.2.7 ElementRef

***Como funciona o ElementRef em componentes***

- O ElementRef funciona como o document em Javascript, permitindo acesso ao DOM;
- Ele é mais específico, permitindo acesso ao DOM do componente.
- Pode ser passado com um ViewChild, ou como uma injeção de dependencia;
- Pode ser injetado dentro de uma diretiva também, para manipulações mais complexas;
- Não podemos fazer a injeção de dependencia de um ElementRef dentro de um service;
- Para usar dentro de um service, devemos passar como parâmetro dentro do método do service;
- Ex.:

```
(component.html)

  <div #minhaDiv></div>

  <div id="minha-outra-div"></div>
  
(component.ts)

  // Usando como viewChild

  @ViewChild('minhaDiv') divEl!: ElementRef<HTMLDivElement>;
  
  ngAfterViewInit() {
    this.divEl.nativeElement.style.backgroundColor = 'orange';
    this.divEl.nativeElement.textContent = 'sou uma div';
    this.divEl.nativeElement.classList.add('minhaDiv');
  }
  
  // Instanciando ElementRef dentro de _elementRef

  constructor(private readonly _elementRef: ElementRef) {
  }

  ngOnInit(): void {
    const divEl = this._elementRef.nativeElement.querySelector('#minha-outra-div') as HTMLDivElement;
    divEl.textContent = 'Sou a outra Div';
    divEl.classList.add('minha-outra-div');
    divEl.style.backgroundColor = 'blue';
    divEl.style.color = 'white';

    divEl.addEventListener('click', () => {
      console.log('Div clicada')
    });
  }
```

## 5.3 Diretivas

### **Por que utilizar diretivas:**

- As diretivas servem para reunir funções e atributos que irão se repetir em vário lugares,
  facilitando a manutenção do código, além de deixar os componentes mais limpos.

### 5.3.1 Como criar diretiva de atributo:

- As diretivas são classes que acessam os atributos e metodos de elementos/componentes que a usam;
- A diretiva @HostBinding() acessa e modifica os atributos de um elemento;
- A diretiva @HostListener() acessa metodos de um elemento, executando funções;
- De forma geral, todos atributos, propriedades e metodos de um elemento que são acessiveis no DOM 
  e com property binding, também são acessíveis pelas diretivas.
- Ex.:

```
(component.html)

  <p directiveName> Component with directive </p>

(directive.ts)
  
  import {Directive, HostBinding, HostListener} from "@angular/core";
  
  
  @Directive({
    selector: '[directiveName]'
  })
  export class directiveNameDirective {
  
    // Acessando a propriedade de background color em styles
    // de todo elemento que usar essa diretiva
    
    @HostBinding('style.background-color') bgColor = 'transparent';
  
    // Acessa um método do elemento, modificando ou acionando
    // alguma função/propriedade de todo elemento que usar a diretiva
    
    @HostListener('mouseover') onMouseOver() {
      this.bgColor = 'orange';
    }
  
    @HostListener('mouseout') onMouseOut() {
      this.bgColor = 'transparent';
    }
  }
```

- Ex. de diretiva para modificar styles:

```

  import {Directive, HostBinding} from '@angular/core';
  
  @Directive({
    selector: '[appStyle]'
  })
  export class StyleDirective {
  
    // Acessando o atributo style
    @HostBinding('attr.style') attrStyle = 'background-color: orange; color: white';
  
    // Acessando a propriedade style, passando uma string
    @HostBinding('style') propStyle = 'background-color: orange; color: white';
  
    // Acessando a propriedade style, passando um objeto
    @HostBinding('style') propStyleObj = {
      backgroundColor: 'orange',
      color: 'white'
    }
  
    // Acessando separadamente duas propriedades de style
    @HostBinding('style.backgroundColor') backgroundColor = 'orange';
    @HostBinding('style.color') color = 'white';
    
    // Nunca acessar a propriedade ngStyle, pode causar problemas
    
  }


```

- Ex. de diretiva para modificar classes:

```

  import {Directive, HostBinding} from '@angular/core';
  
  @Directive({
    selector: '[appClass]'
  })
  export class ClassDirective {
  
    // Acessando o atributo class
    @HostBinding('attr.class') attrClass = 'meu-texto meu-size';
  
    // Acessando a propriedade class, passando uma string
    @HostBinding('className') className = 'meu-texto meu-size';
  
    // Acessando a propriedade class, passando um objeto
    @HostBinding('class') classObj = {
      'meu-texto': true,
      'meu-size': true
    };
  
    // Nunca acessar a propriedade ngClass, pode causar problemas
  
  }


```

- Ex. utilizando eventos:

```

import {Directive, HostListener} from '@angular/core';

  @Directive({
    selector: '[appListener]'
  })
  export class ListenerDirective {
  
    // Captura o evento de click, acionando o método onClick
    @HostListener('click') onClick() {
      console.log('clicou');
    }
  
    // Captura o evento de keyup, passando como parametro para a função onKeyUp
    // o evento (no caso do input, o que foi digitado no evento de keyup) e um segundo
    // parametro fixo, mas que pode ser variável também.
    @HostListener('keyup', ['$event', '"Meu Argumento"']) onKeyUp(event: KeyboardEvent, param2: string) {
      const fullText = (event.target as HTMLInputElement).value;
  
      console.log(fullText);
      console.log(param2);
    }
    
    // Todos eventos disponíveis no DOM e nos métodos de binding do angular
    // podem ser usados nas diretivas do mesmo modo que são usadas dentro
    // dos componentes.
  
  }


```

### 5.3.2 Como passar valores para as Diretivas

- Podemos passar valores de forma estática, como string, e as diretivas funcionando como
  atributos do elemento;
- Podemos passar valores de forma dinâmica, como variáveis, e as diretivas funcionando como
  propriedades do elemento;
- Para receber um valor na diretiva, usamos o @Input();
- Para receber um valor diretamente da diretiva, criamos o @Input com o mesmo nome da diretiva,
  assim, quando chamamos a diretiva no elemento, basta igualá-la ao que gostariamos de passar
  no input;
- Para usar mais de um input, passamos o nome da diretiva e depois o nome do input da diretiva
  que deve ser preenchido, igualado ao seu valor.
- Ex.:

```

(component.html)
  <input
    [appInputBackground] = "backgroundVar"  // passa uma variável - property
    tColor = "white"  // passa uma string - attribute
  >
  
  <input
    appInputBackground = "blue" // passa uma string - attribute
    [tColor] = "colorVar" // passa uma variável - property
  >
  
(component.ts)

  backgroundVar = 'green';
  colorVar = 'gray';
  
(directive.ts)

  import {Directive, HostBinding, HostListener, Input} from '@angular/core';

  @Directive({
    selector: '[appInputBackground]'
  })
  export class InputBackgroundDirectiveDirective {
  
    @Input() appInputBackground: string = 'white';
    @Input('tColor') textColor: string = 'black';
  
    @HostBinding('style.backgroundColor') bgColor: string = '';
    @HostBinding('style.color') color: string = '';
  
    @HostListener('focus') onFocus(): void {
      this.bgColor = this.appInputBackground;
      this.color = this.textColor;
    }
  
    @HostListener('blur') onBlur(): void {
      this.bgColor = 'white';
      this.color = 'black';
    }
  }
```



















