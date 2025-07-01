📘 Principios SOLID en Java
📚 Breve introducción a los Principios SOLID en Java
Una vez que dominamos los fundamentos de la Programación Orientada a Objetos (POO) —como clases, objetos, atributos, métodos, encapsulamiento, constructores y getters/setters—, es importante comenzar a pensar en cómo escribir código limpio, mantenible y escalable.

Ahí es donde entran los principios SOLID.

SOLID es un conjunto de 5 buenas prácticas que te ayudan a construir software más robusto. No necesitas dominarlos al 100% al inicio, pero sí comenzar a entender su propósito.

En la siguiente sección, exploraremos cada principio de forma simple y con ejemplos en Java, para que puedas aplicar estas ideas paso a paso a medida que avanzas como desarrollador.

Los principios SOLID son cinco reglas fundamentales de diseño en la programación orientada a objetos. Fueron definidos por Robert C. Martin ("Uncle Bob") y ayudan a escribir código más limpio, mantenible, escalable y fácil de entender.

A continuación, te presentamos una versión simplificada y didáctica de cada principio, con analogías reales y ejemplos en Java para que puedas comprenderlos fácilmente:

La letra 'S' de 'SOLID' en el desarrollo de software representa el principio de:

Single Responsibility Principle (SRP) o en español: Principio de Responsabilidad Única.

✅ ¿Qué significa? Una clase (o módulo, función, etc.) debe tener una sola razón para cambiar, es decir, una única responsabilidad.

📌 Explicación simple Imagina que tienes una máquina de café que además de hacer café, también imprime facturas y gestiona los turnos de los empleados. Si se rompe algo, no sabes si fue por el café, por la impresora o por el sistema de turnos. Es muy difícil de mantener y arreglar.

En cambio, si tienes:

Una clase para preparar café,

Otra clase para imprimir facturas,

Y otra para gestionar turnos...

Cada una tiene una sola tarea clara, y puedes modificar una sin afectar las otras.

🛠️ En código Java (ejemplo simple) Violando SRP:

java Copiar Editar public class Reporte { public String generarReporte() { // Generar reporte }

public void guardarEnArchivo(String reporte) {
    // Guardar en archivo
}

public void enviarPorEmail(String reporte) {
    // Enviar por email
}
} Aplicando SRP:

java Copiar Editar public class Reporte { public String generarReporte() { // Generar reporte } }

public class Guardador { public void guardarEnArchivo(String reporte) { // Guardar en archivo } }

public class Enviador { public void enviarPorEmail(String reporte) { // Enviar por email } } 🧠 Ventajas de aplicar SRP Código más legible y modular

Fácil de mantener y extender

Menos riesgo de errores al cambiar una parte

O OCP Principio de abierto/cerrado (Open/closed principle) la noción de que las “entidades de software … deben estar abiertas para su extensión, pero cerradas para su modificación”.



La letra 'L' de 'SOLID' representa el principio de:
Liskov Substitution Principle (LSP)
Principio de Sustitución de Liskov

✅ ¿Qué significa?
Las clases derivadas deben poder sustituir a sus clases base sin alterar el comportamiento correcto del programa.

📌 Explicación simple
Imagina que tienes una clase Ave con un método volar(). Luego creas una clase Pingüino que hereda de Ave. Pero... ¡los pingüinos no vuelan! Si alguien usa Pingüino esperando que pueda volar (porque es un Ave), el sistema fallará.

Lo correcto sería repensar la jerarquía para que el comportamiento esperado se mantenga, sin romper el contrato de la clase base.

🛠️ En código Java (violando LSP):

public class Ave {
    public void volar() {
        System.out.println("Estoy volando");
    }
}

public class Pinguino extends Ave {
    @Override
    public void volar() {
        throw new UnsupportedOperationException("¡Los pingüinos no vuelan!");
    }
}



public interface Ave {
    void hacerSonido();
}

public interface AveVoladora extends Ave {
    void volar();
}

public class Gorrion implements AveVoladora {
    public void volar() {
        System.out.println("El gorrión vuela");
    }

    public void hacerSonido() {
        System.out.println("Pío pío");
    }
}

public class Pinguino implements Ave {
    public void hacerSonido() {
        System.out.println("¡Groink!");
    }
}


🧠 Ventajas de aplicar LSP:

Las subclases son seguras de usar sin romper la lógica del programa.

Tu código es más predecible y coherente.

