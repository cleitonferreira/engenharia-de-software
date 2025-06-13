# JavaScript

<img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/javascript/javascript-original.svg" />
          
- [Spread Operator](#spread-operator)

## Spread Operator
O operador spread (...) é uma funcionalidade do JavaScript que permite expandir elementos de arrays ou propriedades de objetos em diferentes contextos.

### Principais Usos do Operador Spread
#### 1. Clonar Arrays
Cria uma cópia superficial de um array.

```javascript
const arrayOriginal = [1, 2, 3];
const arrayClonado = [...arrayOriginal];

console.log(arrayClonado); // [1, 2, 3]
```
#### 2. Concatenar Arrays
Combina dois ou mais arrays em um novo array.

```javascript
const array1 = [1, 2, 3];
const array2 = [4, 5, 6];
const arrayConcatenado = [...array1, ...array2];

console.log(arrayConcatenado); // [1, 2, 3, 4, 5, 6]
```
#### 3. Clonar Objetos
Cria uma cópia superficial de um objeto.

```javascript
const objetoOriginal = { a: 1, b: 2 };
const objetoClonado = { ...objetoOriginal };

console.log(objetoClonado); // { a: 1, b: 2 }
```
#### 4. Mesclar Objetos
Combina as propriedades de dois ou mais objetos em um novo objeto.

```javascript
const objeto1 = { a: 1, b: 2 };
const objeto2 = { b: 3, c: 4 };
const objetoMesclado = { ...objeto1, ...objeto2 };

console.log(objetoMesclado); // { a: 1, b: 3, c: 4 }
```
#### 5. Passar Argumentos para Funções
Expande um array em uma lista de argumentos.

```javascript
const numeros = [1, 2, 3];

function soma(a, b, c) {
  return a + b + c;
}

console.log(soma(...numeros)); // 6
```
### Conclusão
- Clonar Arrays: Use ... para criar cópias de arrays.
- Concatenar Arrays: Combine múltiplos arrays em um novo array.
- Clonar Objetos: Use ... para criar cópias de objetos.
- Mesclar Objetos: Combine propriedades de múltiplos objetos.
- Passar Argumentos para Funções: Expanda arrays para argumentos de função.