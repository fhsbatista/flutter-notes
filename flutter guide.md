## Geral sobre cross-platform
### Vantagens
 - Trabalhar em uma base de código só
   - Isso faz o desenvolvimento mais rápido
   - Menor custo do que trabalhar com um projeto para cada plataforma
   - Consistência em ui e comportamento do app entre as plataformas

### Desvantagens
 - Performance pode ser menor
 - Apps nativos sempre terão uma vantagem que a de poder se comunicar diretamente com o device, sem precisar de intermediários.
 - "Atraso" para atualizar o app com novidades das plataformas
 - Sempre que a plataforma for atualizada com novas coisas, temos que esperar o framework ser atualizado para conseguir dar suporte à essas novidades.
  
## Como o um aplicativo em flutter roda?
O aplicativo em flutter é compilado para ARM (bytecode) (no caso de mobile) ou um "optmized javascript" (no caso da web.)

ARM é um tipo de processador usado em celulares normalmente.

O código dart é convertido diretamente para bytecode (arm), isso faz com que o flutter seja muito rápido e portável para outras plataformas.

### Como um aplicativo se comunica com a plataforma?
Normalmente existe um conjunto de APIs que a plataforma expõe para que o aplicativo poss usar recursos da plataforma. Essas APIs são exclusivas de cada plataforma, não existe compatibilidade entre elas.

No caso do android por exemplo, existe o ART (Android RunTime). O aplicativo se comunica com o ART e o ART se responsabiliza em se comunicar com o sistema operacional Android.
Desta forma, um aplicativo escrito para android de forma nativa, irá estar totalmente dependente do ART e por isso não é compatível com o iOS.

#### Pq é necessário que o app se comunique com a plataforma?
Para poder utilizar serviços como gps, câmera, bluetooth etc. E também para coisas até mais óbvias mas que nem percebemos, por exemplo, fazer algo aparecer na tela! Quando queremos que apareça um botão na tela, precisamos dizer ao sistema operacional que queremos que tal conjunto de pixels na tela fiquem de tal cor, de forma com que ao olhar eles em conjunto vejamos que está desenhado um botão. Claro que na prática, não vamos tanto "baixo nível" assim, mas isso por conta de a plataforma disponibilizar essas APIs que fazem toda essa abstração.

### Como o tecnologias de cross-platform resolvem o problema de compatibilidade entre as plataformas?
Como visto no tópico acima, o sistema operacional é utilizado através de um conjunto de APIs, e essas são as que o aplicativo conversa. Essas APIs são totalmente diferentes dependendo da platfoorma.
Mas como o flutter (ou react native por exemplo), que usa apenas uma base de código consegue gerar um aplicativo que se comunica com as duas plataformas então?

A abordagem vai variar dependendo da tecnologia. Cada tecnologia usa ideias diferentes, e o contexto vai dizer qual tecnologia tem um match melhor com a necessidade.

Mas generalizando, o que acontece é que o framework disponibiliza ao desenvolvedor um conjunto de APIs que vai ser a mesma independente da plataforma. E o framework depois se encarrega de se comunicar com as APIs nativas de cada plataforma depois.

#### React native
No caso do react-native, quem faz essa "intermediação" é uma ferramenta chamada de "bridge". E esta bridge se difere um pouco de outras tecnologias cross-platform. Pois a bridge faz a tradução de o que foi desenvolvido para o uso de widgets, serviços e tudo mais que são nativos da plataforma. Sendo assim, podemos dizer que um aplicativo em "react native" é de certa forma "nativo", pois no final o aplicativo que está rodando está usando todos os recursos nativos da plataforma.

Isso parece um pouco difícil de entender, mas fica fácil entender quando sabemos como que outras tecnologias cross-platform funcionam.
Tecnologias como Ionic, phonegap etc, que eram muito usados antigamente, não gerar aplicativos que se comunicam com as APIs nativas da plataforma por conta da ideia dessas tecnologias. Quando abrimos um aplicativo que foi construído usando essas tecnologias, o que estamos vendo na verdade é uma webview. Então todos os widgets que vemos na tela, estão sendo renderizados através de html/css/javascript. Ou seja, não usa de forma alguma coisas nativas da plataforma. Nesse caso por exemplo, se o usuário atualizar a versão do sistema operacional e esta atualizão tiver mudanças no design dos widgets, o aplicativo feito em ionic ou phonegap não vai seguir essas atualizações, pois as atualizações que foram feitas não impactam nos widgets que estão sendo usados pelo aplicativo nesse caso.

Com isso em mente, agora fica fácil entender pq podemos considerar o react native um pouco "mais nativo" que outras tecnologias, pq ele realmente usa componentes "originais" da plataforma no final de tudo, e não uma webview apenas.

Apesar da forma com que o react trabalha ser interessante, existe um downside importante nessa "bridge" que é uma certa lentidão já que essa bridge acaba se tornando uma espécie de "bottleneck" entre o aplicativo e o sistema operacional.

#### Flutter
O flutter funciona um pouco diferente do reactnative, e em certos aspectos, podemos dizer que o aplicativo em flutter é "menos nativo" do que um escrito em react native se olharmos pelo lado de "usar componentes visuais" nativos da plataforma, pois o react realmente usa os nativos, e o Flutter não.

O jeito de o flutter trabalhar é bem diferente do react native, pois não existe um intermediário como existe no react native.

O flutter roda em cima de uma engine gráfica chamada Skia, e portanto não usa componentes visuais nativos. O sdk do flutter disponibiliza seus próprios componentes visuais e permite o desenvolvedor a criar os seus próprios de uma maneira bem mais fácil.

O flutter gera um código machine code que o ARM vai processar diretamente. Nesse sentido, podemos dizer que o flutter acabe sendo mais "nativo" que o própio react pq ele está acessando o processador diretamente. (Me parece meio estranho essa ideia de interagir com o processador diretamente, pois teoricamente o sistema operacional existe justamente para abstrair isso, então o app deveria estar se comunicando com o sistema operacional ao invés de se comunicar com o processador diretamente, existe uma lacuna aqui, devo ter entendido algo errado).

Uma das grande vantagens do flutter é justamente não depende de componentes visuais nativos das plataformas. O flutter permite que nós tenhamos total liberdade para pintar cada pixel da tela do jeito que bem entendermos.
Uma das grande vantagens do flutter é justamente não depende de componentes visuais nativos das plataformas. O flutter permite que nós tenhamos total liberdade para pintar cada pixel da tela do jeito que bem entendermos.

### Pq o flutter usa o dart?
Existem várias razões, seguem abaixo algumas:
 - Orientada a objetos: Isso deixa o framework mais amigável aos desenvolvedores pois uma grande parte deles já vem desse paradigma de programação.
 - Performance: Boa alocação de memória, confiável.
 - Produtividade: Pelo fato de o dart sem bastante "portável" por poder ser compilada para diferentes plataformas, isso possibilita que usar uma mesma base de código.
 - Ambas tecnologias são da Google: Isso dá muita liberdade para o dart e o flutter irem evoluindo em conjunto, já que as decisões cabem somente à google.
 - É formente tipada: Isso diminui a quantidade de erros em runtime e também deixa o trabalho de debugar muito mais fácil.
 - tree-shaking optimaztion: Isto é um processo que elimina código que não é utilizado. Isso elimina a preocupação no uso de bibliotecas por conta do tamanho do app por exemplo, pois ao compilar, será compilado somente o que realmente pode ser executado. De forma resumida, isso elimina o "dead code".
 - Hot reload: Isso permite que o programa possa ser atualizado sem ter que fazer o build dele inteiro novamente.
 - Suporte para JIT e AOT: O JIT facilita o trabalho em developmente e o AOT facilita o deploy.

## Dart
 - Orientada a objetos
 - "Garbage collected"
 - Roda em qualquer plataforma (não sei direito como isso funciona, por causa da VM talvez?)
 - Possui VM, Dart Virtual Machine

### Inicialização de variáveis
 - O dart não exige que coloquemos o tipo da variável ao declarar ela. Ele consegue descobrir o tipo sozinho de acordo com o tipo dado que foi referenciado nessa variável.
 - Podemos declarar uma variável então com o tipo dela:
  Ex: `String name = 'fernando'`
 - Usar o var:
  Ex: `var name = 'fernando'`
 - Usar o final, o que fará com que esta variável não seja mutável.
  Ex: `final name = 'fernando'`
 - Usar o late, que "atrasa" a inicialização de uma variável (disponível na versão do dart com null safety apenas):
  Ex: 
  `late String name;
  name = 'fernando';`

### Números
Existe um tipo "base" de números que é o `num`. Porém não recomando usá-lo diretamente (exceto em alguns casos que envolvem generics).
O recomendado é trabalharmos com `int` ou `double`, e só tem esses dois mesmo, bem simples até (não tem float, long etc).

#### Boas práticas
Quando for necessário fazer parse de número para string ou o contrário, use os métodos que a classe `num` já tem implementado ao invés de criar um método próprio.
`String value = "17";  
var a = int.parse(value);// String-to-int conversion  
var b = double.parse("0.98");// String-to-double conversion  
var c = int.parse("13", radix: 6);// Converts from 13 base 6 `

`String v1 = 100.toString(); // v1 = "100";  
String v2 = 100.123.toString(); // v2 = "100.123";  
String v3 = 100.123.toStringAsFixed(2); // v3 = "100.12";`

### Strings
 - Podemos usar tanto aspas simples quanto aspas dulpas para declarar uma string
 - Aspas triplas podem ser usadas quando queremos criar uma string em multilinhas. Assim não precisamos ficar usando o `\n`.
 - Não existe o `char`.
 - `StringBuffer` para "montar" strings (ex: StringBuilder no java);

### Enums
Enums são uma ótima maneira de abstrair "opções" de algo de forma a fazer com que o compilador nos ajuda.
Por exemplo, tipos de combustível. Ao invés de em um método que calcula algo de um combustível nós passarmos um int por exemplo para cada combustível, podemos usar um enum. Isto faz com que não tenhamos que ficar checando se um int é um int válido e tal.

```
enum Fuel { gasoline, etanol, diesel }

void calcFuel(Fuel item)... // GOOD - não precisamos ficar checando se o item é um combustível válido!
  
void calcFuel(int item)... // BAD - vamos ter que ficar checando se o int passado é válido para poder trabalhar com ele de forma segura.
```

### Booleans
Nenhum segredo aqui.
ex:
```
bool isValid = true;
```

### Arrays e Lists
Em dart, diferente de java ou c#, não existe um tipo "array" puramente dito. No dart temos colections, e a mais básica delas é a `List`, e funciona como um array.
ex:
```
List<int> ints = <int>[] ou List<int>()
```
O bom de trabalhar com `List` é esta collection já expõe pra nós muitos métodos úteis para o dia a dia, como `add()`, `remove()`, `contains(T element)` e etc.

### Nullability
 - Por enquanto, não está disponível em nenhuma versão stable do dart.
  - Primeira tech-preview saiu em junho/2020, e a segunda em outubro/2020 (esta segunda com suporte para flutter).
 - Disponível a partir do dart 2.10.
 - Variáveis são "não nullables" por default.
 - Com o null-safety ativado, vc pode até declarar uma variavel e não inicializar, mas o compilador já consegue reconhecer isso e te avisar, evitando assim então uma surpresa em runtime.
 - Para dizer que algo deve sim ser "nullable", basta colocar o "?" como sufixo do tipo, como `int? teste;`
 - Para afirmar que uma variável nullable não vai estar nula em determinado momento, use-o "bang operator", que é o "!" (igual o kotlin);
 - Para um "fallback" ao usar um nullable, use o `??` para passar o valor default ex:

 ```` val teste = x ?? y;````
 - Para acessar propriedades de um nullable, vc precisa usar o "?." ao invés de "?""
````val teste = x?.cor;````

### Operadores 
#### Aritméticos (adição, subtração etc)
Em dart, os operadores são basicamentes os mesmos que os usados emo outras linguages.
 - `+` -> adicião
 - `-` -> subtração
 - `*` -> multiplicação
 - `/` -> divisão
 - `%` -> módulo
 - `~/` -> divisão arredondada (ex: 9 ~/ 2 : 4 (e não 4.5))

 Temos também os operadores que modificam uma variável:
 ex:
 ````
 ++a;
 a++;

 --a;
 a--;

 int b = 1;
 b += 3;
````
Obs: o ++ (ou --) antes da variável e depois da variável funcionam de forma diferente, mas ambos iram incrementar `1` na variável.
 - ++a -> é incrementado 1 e depois retornado o valor;
 - --a -> é retornado o valor e depois incrementado 1;
 Parecem ser a mesma coisa, mas isto pode ser causa de problemas quando não estamos atentos a isso.

#### Relacionais
São basicamente os mesmos de qualquer outra linguagem: ==, !=, >, <, >=, <=

### Tipos
Para trabalhar em cima de tipos das variávels: as, is e is!

Observação importante:
 - Se vc estiver dentro do escopo de um if, o qual a condição é um `is`, vc não precisa ficar fazendo casting (as) na variável em questão por que o compilador já entende aquele escopo não precisa de cast nesse caso.
 `````
 if (apple is fruit) {
   print(apple.nutrients); //não precisou fazer algo como (apple as fruit).nutrients
 }
`````





### Formas de distribuir em programa em dart
 - Stand-alone: 
   - Um programa que vai rodar na DVM (Dart virtual machine). 
   - Sendo assim, é necessário que a plataforma possua essa DVM.
   - Este tipo de compilacão é o usado em fase de desenvolvimento.
   - Este tipo de compilacão usa a estratégia JIT (just in time), que é um tipo de compilacão dinâmica que acontece enquando o programa está rodando. É o que possibilita atualizarmos o código enquanto o programa (app por exemplo) ainda está rodando, sem ter que fazer o build da aplicacão novamente.
 - AOT (ahead of time)
   - O programa em dart é convertido diretamente para um código de máquina nativo em x64.
   - Dispensa o uso da DVM para ser executado já que o código gerado é um native machine code.
   - A ferramenta do dart que faz essa compilacão é o `dart2native` (a partir da versão 2.6).
   - Este tipo de compilacão é o usado para deploy.
 - Web
   - O código em dart pode ser "transpilado" para um javascript otimizado
   - Isto faz com que o flutter possa rodar em navegadores como firefox e chrome, usando o mesmo código dart que já roda em outras plataformas (ios, android ou desktop)
   - A ferramenta do dart que faz essa "transpilacão" é o `dart2js`.

### SDK
 - dart2js: compila o dart para javascript
 - pub: package manager
 - dartdoc e dartfmt: ainda não sei a importância, mas parecem não ser importantes mesmo.

## Packages
Além de pacotes que já vêm com o dart (dart:io, dart:collection etc), podemos conseguir novos packages pelo pub.io.
Este site é onde ficam publicados diversos packages criados pelo time do dart, flutter e da comunidade. Neste mesmo site existem pacotes tanto para dart quando para flutter.

## Primeiros passos
### Hello world
Um bom lugar para fazer o hello world é pelo dartpad.dev.
É como se fosse um editor de texto (não IDE) online, que te permite criar um projeto tanto para dart quanto para flutter.
Atencão: Esta é uma ferramenta muito limitada e é útil apenas para um primeiro contato, ou testar alguma coisa da linguagem etc. Não é possível fazer testes ou deploy com o dartpad.

## IDEs
Para desenvolver com dart/flutter, você pode usar o intelliJ, android studio, vscode e outros (inclusive o vim se não me engano.)
Basta baixar o plugin do dart pelo marketplace da IDE, e também o plugin do flutter caso sua intencão seja desenvolver algo em flutter.


# Termos
Aqui vou ir anotando o que significam alguns termos que eu não sabia o significado conforme eu leio o livro.

 - standalone: um programa que pode ser executado independente de outros programas ou plataforma, ele necessita apenas do sistema operacional.
 - ahead of time (aot): é um tipo de compilacão que transforma o código fonte em bytecode.
 - bytecode: código intermediário **entre** o que o **programador escreve** e o que o **processador entende**. É o tipo de código que **máquinas virtuais** entedem.
 - ARM: arquitetura de processadores RISC, muito usado em celulares pelo baixo custo, não esquentam muito e consomem pouca energia.
 - RISC: (Reduced Instruction Set Computer), basicamente é uma forma de denominar o tipo de instrucões que os processadores ARM entendem.
