## Sección 2: JavaScript

1. **Pregunta Teórica:**
- Explica la diferencia entre var, let y const en JavaScript.
   var: Tiene alcance de función y puede ser redeclarada y reasignada.
   let: Tiene alcance de bloque y puede ser reasignada, pero no redeclarada en el mismo ámbito.
   const: Tiene alcance de bloque y no puede ser reasignada ni redeclarada.

1. **Pregunta de Código:**
- Escribe una función en JavaScript que invierta una cadena de texto.
    function reverseString(str) {
    return str.split('').reverse().join('');
    }

    console.log(reverseString("hello")); // "olleh"


1. **Pregunta Teórica:**
- ¿Qué es el Event Loop en JavaScript y cómo funciona?
    Event Loop: Es un mecanismo que maneja la ejecución de código, la recopilación de eventos y la ejecución de sub-tareas en un ciclo continuo. Permite que JavaScript sea no bloqueante y asíncrono. Funciona verificando la pila de llamadas y la cola de mensajes, procesando los mensajes de la cola cuando la pila está vacía.

1. **Pregunta de Código:**
- Escribe un script en JavaScript que filtre los números pares de un array de números y los muestre en la consola.
    const numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

    const evenNumbers = numbers.filter(num => num % 2 === 0);

    console.log(evenNumbers); // [2, 4, 6, 8, 10]


1. **Pregunta Teórica:**
- ¿Qué es el DOM y cómo se manipula usando JavaScript?
    DOM (Document Object Model): Es una representación estructural de un documento HTML. Permite a los lenguajes de programación acceder y manipular el contenido, estructura y estilo del documento.
    Manipulación del DOM: Se realiza utilizando métodos como getElementById, querySelector, createElement, appendChild, y propiedades como innerHTML, textContent, style, etc.

1. **Pregunta de Código:**
- Escribe un código en JavaScript que añada un event listener a un botón con el id #myButton para mostrar una alerta con el mensaje "Hello World" al hacer clic.
    document.getElementById('myButton').addEventListener('click', function() {
        alert('Hello World');
    });


1. **Pregunta Teórica:**
- Explica qué es una Promesa en JavaScript y proporciona un ejemplo básico.
    Promesa: Es un objeto que representa la eventual finalización (o falla) de una operación asíncrona y su valor resultante. Las promesas pueden estar en tres estados: pendiente, cumplida o rechazada.
    Codigo:
    const myPromise = new Promise((resolve, reject) => {
        let success = true;
        if (success) {
            resolve("Operation successful");
        } else {
            reject("Operation failed");
        }
    });

    myPromise.then(result => {
        console.log(result);
    }).catch(error => {
        console.log(error);
    });


1. **Pregunta de Código:**
- Escribe una función en JavaScript que haga una petición AJAX (usando fetch) para obtener datos de una API y los muestre en un elemento con el id #result.
    async function fetchData() {
        try {
            const response = await fetch('https://api.example.com/data');
            const data = await response.json();
            document.getElementById('result').textContent = JSON.stringify(data);
        } catch (error) {
            console.error('Error fetching data:', error);
        }
    }

    fetchData();


1. **Pregunta Teórica:**
- ¿Cuál es la diferencia entre null, undefined y NaN en JavaScript?
    null: Representa la ausencia intencional de cualquier valor.
    undefined: Indica que una variable ha sido declarada pero no tiene un valor asignado.
    NaN: Significa "Not-a-Number" y es el resultado de operaciones matemáticas que no tienen sentido numérico (como 0/0).

1.  **Pregunta de Código:**
- Implementa una función en JavaScript que use localStorage para guardar una clave-valor y luego recuperarla.
    function saveToLocalStorage(key, value) {
        localStorage.setItem(key, value);
    }

    function getFromLocalStorage(key) {
        return localStorage.getItem(key);
    }

    // Ejemplo de uso
    saveToLocalStorage('username', 'Yoan');
    console.log(getFromLocalStorage('username')); // "Yoan"