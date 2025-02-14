# challenge-amigo-secreto_alura
El siguiente codigo se realizó como desafio del curso de Alura, para lenguaje de javascript

Se utilizó ayuda de inteligencia artificial QWen 2.5 Max:

Agregar Amigo (agregarAmigo):
-Esta función obtiene el valor del input donde se escribe el nombre del amigo.
-Valida que el nombre no esté vacío.
-Agrega el nombre al array amigos.
-Limpia el input después de agregar el nombre.
-Actualiza la lista visible de amigos llamando a la función actualizarListaAmigos.

Actualizar Lista de Amigos (actualizarListaAmigos):
-Esta función limpia la lista actual de amigos en el DOM.
-Recorre el array amigos y crea elementos <li> para cada nombre, añadiéndolos a la lista.
-Sortear Amigo (sortearAmigo) :
-Verifica que haya al menos 2 amigos para realizar el sorteo.
-Crea una copia del array amigos para evitar modificar el original.
-Realiza un sorteo aleatorio asignando un amigo secreto a cada amigo, asegurándose de que nadie sea su propio amigo secreto.
-Muestra los resultados llamando a la función mostrarResultados.

Mostrar Resultados (mostrarResultados):
-Esta función limpia los resultados anteriores.
-Recorre el array de resultados y crea elementos <li> para cada par de amigo y amigo secreto, añadiéndolos a la lista de resultados.

Reto javascript curso Alura

// Array para almacenar los nombres de los amigos ingresados
let amigos = [];

/**
 * Función para agregar un amigo a la lista.
 */
function agregarAmigo() {
    // Obtener el valor del input
    const inputAmigo = document.getElementById('amigo');
    const nombreAmigo = inputAmigo.value.trim();

    // Validar que el nombre no esté vacío
    if (nombreAmigo === '') {
        alert('Por favor, ingresa un nombre válido.');
        return;
    }

    // Agregar el nombre al array de amigos
    amigos.push(nombreAmigo);

    // Limpiar el input
    inputAmigo.value = '';

    // Actualizar la lista visible de amigos
    actualizarListaAmigos();
}

/**
 * Función para actualizar la lista visible de amigos en el DOM.
 */
function actualizarListaAmigos() {
    const listaAmigosElement = document.getElementById('listaAmigos');
    listaAmigosElement.innerHTML = ''; // Limpiar la lista actual

    // Crear elementos <li> para cada amigo y añadirlos a la lista
    amigos.forEach((amigo, index) => {
        const li = document.createElement('li');
        li.textContent = amigo;
        listaAmigosElement.appendChild(li);
    });
}

/**
 * Función para realizar el sorteo de amigos secretos.
 */
function sortearAmigo() {
    // Validar que haya al menos 2 amigos para realizar el sorteo
    if (amigos.length < 2) {
        alert('Debes ingresar al menos 2 amigos para realizar el sorteo.');
        return;
    }

    // Crear una copia del array de amigos para evitar modificar el original
    const amigosCopia = [...amigos];

    // Realizar el sorteo aleatorio
    const resultados = [];
    while (amigosCopia.length > 0) {
        const indiceAmigo = Math.floor(Math.random() * amigosCopia.length);
        const amigo = amigosCopia.splice(indiceAmigo, 1)[0];

        // Elegir un amigo secreto diferente al amigo actual
        const indiceAmigoSecreto = Math.floor(Math.random() * amigosCopia.length);
        const amigoSecreto = amigosCopia[indiceAmigoSecreto] || amigos[Math.floor(Math.random() * amigos.length)];

        resultados.push(`${amigo} -> ${amigoSecreto}`);
    }

    // Mostrar los resultados en el DOM
    mostrarResultados(resultados);
}

/**
 * Función para mostrar los resultados del sorteo en el DOM.
 * @param {Array} resultados - Array con los resultados del sorteo.
 */
function mostrarResultados(resultados) {
    const resultadoElement = document.getElementById('resultado');
    resultadoElement.innerHTML = ''; // Limpiar resultados anteriores

    // Crear elementos <li> para cada resultado y añadirlos a la lista
    resultados.forEach(resultado => {
        const li = document.createElement('li');
        li.textContent = resultado;
        resultadoElement.appendChild(li);
    });
}
