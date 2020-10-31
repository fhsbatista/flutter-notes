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

## Dart
 - Orientada a objetos
 - "Garbage collected"
 - Roda em qualquer plataforma (não sei direito como isso funciona, por causa da VM talvez?)
 - Possui VM, Dart Virtual Machine

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




