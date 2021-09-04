# Estudo-Teorico-JS

### Estudando teorias 🧠


### JS 
- [Como funciona o JS](#how-js-works)
- [O que é o JS](#what-is-js)
- [Scope](#scope)
- [Nested Scopes](#nested-scopes)
- [Variables](#variables)
- [ES6 Features](#es6-features)
- [Pure Functions](#pure-functions)
- [Closure](#closure)
- [Currying](#currying)
- [Higher-Order Functions](#higher-order-functions)

#### <a name="how-js-works"></a> Como funciona o JS
O google chrome usa a engine v8 (open source escrita em c++) . A engine v8 serve para interpretar um código javascript. 
A v8 foi projetada para aumentar a perfomance de execução do JS dentro de navegadores, ele compila código JS em código de maquina ao invés de usar um interpretador. Ele compila de js para código de máquina em tempo de execução, implementando um compilador JIT (just in time).

```JS => c++ => Assembly => Machine Code ```

#### <a name="what-is-js"></a> O que é o JS
Javascript é como nós chamamos a linguaguem (mas isso é o trademark da Oracle), o nome oficial da linguagem é ECMAScript (ES) é a abreviação. 


fontes:
- [https://medium.com/@matheusml/o-guia-do-es6-tudo-que-voc%C3%AA-precisa-saber-8c287876325f](https://medium.com/@matheusml/o-guia-do-es6-tudo-que-voc%C3%AA-precisa-saber-8c287876325f)
- [https://pt.wikipedia.org/wiki/Interpretador_de_JavaScript](https://pt.wikipedia.org/wiki/Interpretador_de_JavaScript)
- [https://pt.stackoverflow.com/questions/383174/o-ecmascript-6-%C3%A9-suportado-pelos-browsers-atuais](https://pt.stackoverflow.com/questions/383174/o-ecmascript-6-%C3%A9-suportado-pelos-browsers-atuais)


####  <a name="scope"></a>Scope
Escopo é a acessibilidade de objetos, variáveis e funções em diferentes partes do código.

- Escopo Global
	- Uma variável global é definida quando declaramos uma variável fora de qualquer função, assim ela torna **acessível a qualquer parte** da nossa aplicação ou site, podendo ser lida e alterada.

- Escopo Local
	- Uma variável se torna local quando ela é declarada dentro de uma função, de tal maneira a qual ela somente estará **acessível dentro dessa função**.
	
- Escopo de bloco
	- Não existia no JS escopo de bloco. Ou seja, for whiles e ifs não tinham escopo próprio. Porém com o ECMAScript 6 foi possível criar escopos de bloco usando as variáveis **let** e **const**, que são **acessíveis somente dentro do bloco.**

#### <a name="nested-scopes"></a> Nested Scopes

Todo o escopo é fechado para acessos externos, de forma que escopos superiores não conseguem acessar escopos internos, mas o contrário é permitido.

``` javascript 
function foo() {
    function bar() {
    
    }
}
```

Quando criamos outra função dentro da função foo, estamos colocando outra caixa dentro do escopo da função, criando o que é chamado de “nested scopes”, ou escopos aninhados.


#### <a name="variables"></a> Variables (var, let e const)

- Var 
	-    é içada
	-   tem escopo abrangente → se for declarada dentro de um bloco → vaza do escopo
	-   escopo global e função → n tem escopo de bloco
	- Praticamente não são mais usadas em aplicações modernas devidos aos problemas de escopo → **substituídas por const e lets**
  
```javascript
function foo (a) {
  var name = 'Lucas'
  
  function bar () {
    var age = 23
    console.log(name) // Luca
    console.log(age) // 23
  }
  
  bar() // Lucas - 23
  console.log(name) // Lucas
  console.log(age) // age is not defined
}
```

```javascript
if(true) {
    var global = 2; // vaza de dentro do bloco
}

function teste() {
    var global = 4;
    console.log(global); //4
}

console.log(global); //2 -> acessa a que vazou do if
``` 

- Let e Const
	-   Tem escopo de **bloco** e de função
	-  Sofrem hoisting (são elevadas) para o topo do bloco que foram definidas → porém não é atribuido o valor de undefined como acontece com var  → continuam não inicializadas e dão erro caso sejam chamadas antes de suas declarações.
	- A grande diferença entre as duas é que consts não podem ser reatribuídas enquanto lets sim.

```javascript
function name() {
	console.log(name); // ❌ retorna erro porque ainda não foi inicializada
	let name = 'isadora';
	console.log(name); // 👍🏼 isadora
	name = 'isadora 2'; // 👍🏼 pode ser reatruída
}

const num = 6;
num = 8; // ❌ Não pode ser reatribuída porque é const

```
	
#### <a name="es6-features"></a> ES6 Features

- Declaração de variáveis
- Default Parameters
- Rest parameters
- Programação funcional => arrow functions
- Destructing
- Classes (constructor, get/setters, herança (extends))
- Es6 Modules (import, export)

fonte: [https://medium.com/@matheusml/o-guia-do-es6-tudo-que-voc%C3%AA-precisa-saber-8c287876325f](https://medium.com/@matheusml/o-guia-do-es6-tudo-que-voc%C3%AA-precisa-saber-8c287876325f)

#### <a name="pure-functions"></a> Pure Functions
- Dada a mesma entrada, vai sempre retornar a mesma saída
- Não produz nenhum efeito colateral
```javascript
functions pureFunction(a,b) {
	return a + b;
} 
pureFunction(1,2) // retorna 3
 ```
 - Retorna sempre o mesmo valor baseado na entrada e não manipula nenhuma variável de fora.
 - Porque usar?
	 - Mais fáceis de implementar e testar
	 - Código mais limpo, prático e de simples manutenção
 
#### <a name="currying"></a> Currying
```Currying é o nome dado à técnica de dividimos uma função que recebe vários argumentos numa série de funções cada uma lidando com **um** argumento da função inicial.```

- Forma de injetar os parametros de forma parcial. 
- É uma função normal
- Faz parte de programação funcional
- Transforma uma função com múltiplos argumentos em uma sequencia de nested functions (função aninhada). Ela retorna uma função que espera os próximos argumentos.

```javascript
function somap(a) {
    return function(b) {
        return a+b
    }
}

// Uso:
var somadois = somap(2);
somadois(3); // 5
 ```
também podemos executa-lá de uma vez fazendo:
```somap(2)(3) // retorna 5 ```

também pode ser escrita usando arrow functions: 
```javascript
const myFunction = valor1 => valor2 => valor3 => {
	return valor1 + valor2 + valor3;
}

console.log(myFunction(1)) // retorna a função esperando o segundo parametro
console.log(myFunction(2)(4)(3)) // retorna 8
```

#### <a name="higher-order-functions"></a> Higher-Order Functions
- É uma função que **recebe como parâmetro** outra função e/ou que **retorna** uma função
- Ex: map, reduce, filter..
 
```javascript
// calculate recebe como parametro uma função
// calculate retorna uma função
// Higher-Order function
var calculate = function(fn, x, y) {
	return fn(x, y);
};

var sum = function(x, y) {
	return x + y;
};

var mult = function(x, y) {
	return x * y;
};

calculate(sum, 2, 5); // 7
calculate(mult, 2, 5); // 10
 ```
usando ES6:
```javascript
const calculate = (fn, x, y) => fn(x,y);
const sum = (x, y) => x + y;
const mult = (x, y) => x * y;
calculate(sum, 2, 5); // 7
calculate(mult, 2, 5); // 10
 ```

#### <a name="closure"></a> Closure
- Closure é a forma de fazer com que as variáveis dentro de uma função sejam **privadas** e **persistentes**.
- Se refere à forma como funções definidas dentro de um "contexto léxico" (i.e. o corpo de uma função, um bloco, um arquivo fonte) acessam variáveis definidas nesse contexto.

```javascript
function pai(){  
   var x = 1;  
   function filho(){  
	  console.log(x);  
	  x++;  
   }  
   return filho;  
}  
  
var contador = pai();  
contador(); // 1  
contador(); // 2  
contador(); // 3
```
```A função filho possui uma referência ao escopo da função pai, e a essa referência nós damos o nome de closure.```

- Módulos são estruturas de código que fazem bom uso das _closures_, vamos a um exemplo que apresenta bem seu funcionamento:
```javascript
 function ModuloMatematico() {       
    var x = 0;      
    function somaUm() {  
        x++;          
        console.log(x);       
    }
    function subtraiUm() {           
        x--;  
        console.log(x);       
    }
	return {           
        somaUm: somaUm,           
        subtraiUm: subtraiUm       
    };   
}
var teste = ModuloMatematico();    
teste.somaUm();     // 1   
teste.somaUm();     // 2  
teste.somaUm();     // 3  
teste.subtraiUm();  // 2
```
Nesse exemplo, não seria possível acessar diretamente X, porém usando closures é possível fazer isso.
