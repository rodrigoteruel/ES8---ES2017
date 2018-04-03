# ES8---ES2017

## STRING PADDING

Essa sessão adiciona duas funções ao objeto String: padStart e padEnd. Como o nome já diz, a razão dessas funções é preencher o começo ou o final de uma string, resultando que a string contenha o tamanho especificado. Você pode preencher com um determinado símbolo ou string, ou por padrão, com espaços. Aqui alguns exemplos:

str.padStart(targetLength [, padString])

str.padEnd(targetLength [, padString])

Como você pode ver, o primeiro parâmetro dessas funções é o targetLength, esse é o tamanho total que o resultado terá. O segundo parâmetro é o padString, que é opcional, esse é o símbolo que irá ser usado para preencher os espaços. O valor padrão é um espaço em branco.

'es8'.padStart(2);          // 'es8'

'es8'.padStart(5);          // '  es8'

'es8'.padStart(6, 'woof');  // 'wooes8'

'es8'.padStart(14, 'wow');  // 'wowwowwowwoes8'

'es8'.padStart(7, '0');     // '0000es8'

'es8'.padEnd(2);          // 'es8'

'es8'.padEnd(5);          // 'es8  '

'es8'.padEnd(6, 'woof');  // 'es8woo'

'es8'.padEnd(14, 'wow');  // 'es8wowwowwowwo'

'es8'.padEnd(7, '6');     // 'es86666'  



## OBJECT.VALUES E OBJECT.ENTRIES

O método Object.values retorna um array de valores das propriedades enumeráveis do dado objeto, na mesma ordem que um for in loop. A declaração é:

Object.values(obj)

O parâmetro obj, é o objeto origem para a operação. Pode ser tanto um objeto, ou, um array (que é simplesmente, um objeto com índices, ex: 

[10, 20, 30] = { 0: 10, 1: 20, 2: 30 }).

const obj = { x: 'xxx', y: 1 };

Object.values(obj); // ['xxx', 1]

// mesmo que { 0: 'e', 1: 's', 2: '8' };

const obj = ['e', 's', '8']; 

Object.values(obj); // ['e', 's', '8']

// se você usar chaves com valores numéricos, o array retornado

// será ordenado de acordo com elas

const obj = { 10: 'xxx', 1: 'yyy', 3: 'zzz' };

Object.values(obj); // ['yyy', 'zzz', 'xxx']

Object.values('es8'); // ['e', 's', '8']

Suporte atual dos navegadores para Object.values

Suporte atual dos navegadores para Object.values

O Object.entries retorna um array das propriedades enumeráveis de um dado objeto em pares [chave, valor], na mesma ordem que Object.values. A declaração é:

const obj = { x: 'xxx', y: 1 };

Object.entries(obj); // [['x', 'xxx'], ['y', 1]]

const obj = ['e', 's', '8'];

Object.entries(obj); // [['0', 'e'], ['1', 's'], ['2', '8']]

const obj = { 10: 'xxx', 1: 'yyy', 3: 'zzz' };

Object.entries(obj); // [['1', 'yyy'], ['3', 'zzz'], ['10': 'xxx']]

Object.entries('es8'); // [['0', 'e'], ['1', 's'], ['2', '8']]

Suporte atual dos navegadores para Object.entries

Suporte atual dos navegadores para Object.entries

## OBJECT.GETOWNPROPERTYDESCRIPTORS

O método getOwnPropertyDescriptors retorna a propriedade descriptor do objeto especificado. A propriedade descriptor é definida diretamente no objeto e não é herdada através do prototype de objetos. A declaração é a seguinte:

Object.getOwnPropertyDescriptor(obj, prop)

O parâmetro obj, é o objeto origem para a operação e o prop, é o nome da propriedade a ser buscada. Os resultados possíveis são: configurable, enumerable, writable, get, set e value.

const obj = { get es8() { return 888; } };

Object.getOwnPropertyDescriptor(obj, 'es8');

// {

//   configurable: true,

//   enumerable: true,

//   get: function es8(){}, // a função get

//   set: undefined

// }

Essa descrição de dados é muito importante para outras funcionalidades, uma delas, o DECORATORS.

Nota: Se quiser saber mais detalhes de implementação sobre decorators, RECOMENDO ESSE ARTIGO EM INGLÊS.


## TRAILING COMMAS EM PARÂMETROS OU INVOCAÇÕES DE FUNÇÕES

Trailing commas em parâmetros de uma função trás a habilidade para o compilador não retornar um error (SyntaxError) quando for adicionado uma vírgula no final de uma lista de parâmetros:

function es8(var1, var2, var3,) {

  // ...
  
}

O mesmo ocorre para a invoação da função:

es8(10, 20, 30,);

Essa novidade é inspirada em objetos literais e arrays, como: [10, 20, 30,] e { x: 1, }.

## FUNÇÕES ASYNC

A função async define uma função assíncrona, que retorna um objeto AsyncFunction. Internamente, funções async funcionam parecidas com GENERATORS, porém, elas não são convertidas em um.

function fetchTextByPromise() {

  return new Promise(resolve => { 
  
    setTimeout(() => { 
    
      resolve("es8");
      
    }, 2000));
    
  });
  
}

async function sayHello() { 

  const externalFetchedText = await fetchTextByPromise();
  
  console.log(`Hello, ${externalFetchedText}`); // Hello, es8
  
}

sayHello();

O resultado de sayHello, Hello, es8, será mostrado depois de 2 segundos.

console.log(1);

sayHello();

console.log(2);

Resultando em:

1 // síncrono

2 // síncrono

Hello, es8 // depois de 2 segundos

Isso é porque a função não bloqueia o fluxo de execução do JavaScript.

Preste atenção que, uma função async, sempre retorna uma Promise, e a palavra chave await, só pode ser usada em funções marcadas com async.

## COMPARTILHAMENTO DE MEMÓRIA E ATOMICS

Quando compartilhamos memória, múltiplas threads podem ler e escrever no mesmo dado em memória. Operações Atomic trazem a garantia de que, essas operações de escrita e leitura, sejam previsíveis, ou seja, a operação é finaliza antes da próxima operação começar e, essas operações, não pode ser interrompidas. Introduzindo novos construtores como SharedArrayBuffer e um objeto global Atomic com métodos estáticos.

O objeto Atomic, é um objeto estático, como o Math, dessa maneira, não podemos usar ele como um construtor. Alguns exemplos dos métodos disponíveis:

add / sub – adicionar ou subtrair um valor de um valor em uma posição específica

and, or, xor – bitwise and / bitwise or / bitwise xor (mais detalhes sobre BITWISE NA MDN).

load – busca o valor em uma posição específica



## E PARA O PRÓXIMO ANO, NO ES9, MELHORANDO RESTRIÇÕES EM TEMPLATE LITERALS

Com os TAGGED TEMPLATE LITERAL do ES6, nós podemos declarar uma função para analisar um determinado template e retornar valores de acordo com nossa lógica:

function helper(strs, ...keys) {

  const str1 = strs[0]; // ES
  
  const str2 = strs[1]; // is
  
  let additionalPart = '';
  
  if (keys[0] == 8) { // 8
  
    additionalPart = 'awesome';
    
  }
  
  else {
  
    additionalPart = 'good';
    
  }

  return `${str1} ${keys[0]} ${str2} ${additionalPart}.`;
  
}

const esth = 8;

helper`ES ${esth} is `;

O valor retornado é: ES 8 is awesome. Se mudarmos o esth para 7, o valor seria: ES 7 is good.

Porém, há uma restrição para templates contendo sub-strings com \u ou \x. ES9 irá resolver esse problema. Você pode saber mais detalhes no MDN ou no TC39.

