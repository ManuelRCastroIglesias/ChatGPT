# ChatGPT
Utilerías para ChatGPT

## Cómo ajustar bloques de código en ChatGPT  
### Introducción  
Este artículo explica cómo ajustar bloques de código en ChatGPT para mejorar la legibilidad y la experiencia del usuario.  
### Requisitos previos  
1.	Descargar e instalar Tampermonkey desde este enlace https://www.tampermonkey.net/  
2.	Suscribirse al plan gratuito de Tampermonkey.  
Pasos para implementar  
1.	Abre Tampermonkey en tu navegador.  
2.	Haz clic en 'Crear un nuevo script'.  
3.	Copia y pega el siguiente **código de javascript** en el editor:  
  ```javascript  
  // ==UserScript==  
  // @name         Ajustar bloques de código en el chat  
  // @namespace    http://tampermonkey.net/  
  // @version      0.1  
  // @description  Cambia la fuente y el tamaño de los bloques de código en la ventana del chat  
  // @author       Manuel Rosendo Castro Iglesias, Asistente: ChatGPT versión [tu versión]  
  // @match        https://chat.openai.com/*  
  // @grant        none  
  // ==/UserScript==  
    
  (function() {  
    'use strict';  
  
    // Función para dividir líneas largas  
    const splitLongLines = (text, maxLen) => {  
        const lines = text.split('\n');  
        return lines.map(line => {  
            if (line.length <= maxLen) return line;  
            let result = '';  
            let lineLen = 0;  
            line.split(' ').forEach(word => {  
                if (lineLen + word.length + 1 > maxLen) {  
                    result += '\n';  
                    lineLen = 0;  
                }  
                result += (lineLen > 0 ? ' ' : '') + word;  
                lineLen += word.length + 1;  
            });  
            return result;  
        }).join('\n');  
    };  
  
    // Función para aplicar los estilos deseados  
    const adjustCodeBlocks = () => {  
        const codeBlocks = document.querySelectorAll('code');  
        codeBlocks.forEach((block) => {  
            block.style.fontFamily = 'monospace';  
            block.style.fontSize = '16px';  
            block.textContent = splitLongLines(block.textContent, 80);  
        });  
    };  
  
    // Escuchar el atajo de teclado Ctrl+Alt+K  
    document.addEventListener('keydown', (e) => {  
        if (e.ctrlKey && e.altKey && e.code === 'KeyK') {  
            adjustCodeBlocks();  
        }  
    });  
}  )();  
  ```  
  
### Guarda los cambios.  
### Recarga la página de ChatGPT.  
  
    Con estos pasos, deberías ser capaz de ver los bloques de código ajustados en ChatGPT.  
## Conclusión  
Este script es una solución rápida y efectiva para mejorar la legibilidad de los bloques de código en ChatGPT. Sin embargo, aún falta implementar el mantenimiento de los colores de sintaxis.  
