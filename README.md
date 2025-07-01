# Principios SOLID en Java #
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

La letra 'O' de 'SOLID' en el desarrollo de software representa el principio de:
Open/Closed Principle (OCP) o en español: Principio Abierto/Cerrado.

✅ ¿Qué significa? Las entidades de software (clases, módulos, funciones, etc.) deben estar abiertas para extensión pero cerradas para modificación. Esto significa que el comportamiento de una clase debe ser extensible sin modificar su código fuente.

📌 Explicación simple Imagina que tienes una aplicación de procesamiento de imágenes que puede aplicar filtros a las imágenes. Si quieres agregar un nuevo filtro, no deberías tener que modificar el código existente. En su lugar, deberías poder extender la funcionalidad existente sin tocar el código original.

En cambio, si tienes:

Una clase base que define una interfaz para aplicar filtros,

Y clases derivadas para cada tipo de filtro específico...

Puedes agregar nuevos filtros simplemente creando nuevas clases derivadas sin modificar la clase base.

🛠️ En código Java (ejemplo simple)

Violando OCP:

java

public class ImageProcessor { public void applyFilter(Image image, String filterType) { if ("brightness".equals(filterType)) { // Aplicar filtro de brillo } else if ("contrast".equals(filterType)) { // Aplicar filtro de contraste } // Más filtros... } }

Aplicando OCP:

java

public interface Filter { void apply(Image image); }

public class BrightnessFilter implements Filter { public void apply(Image image) { // Aplicar filtro de brillo } }

public class ContrastFilter implements Filter { public void apply(Image image) { // Aplicar filtro de contraste } }

public class ImageProcessor { private List filters = new ArrayList<>();

public void addFilter(Filter filter) {
    filters.add(filter);
}

public void applyFilters(Image image) {
    for (Filter filter : filters) {
        filter.apply(image);
    }
}
}

🧠 Ventajas de aplicar OCP

Código más modular y reutilizable: Puedes extender la funcionalidad sin modificar el código existente.
Menos riesgo de introducir errores: Al no modificar el código existente, reduces el riesgo de introducir nuevos errores.
Fácil de mantener y extender: Puedes agregar nuevas funcionalidades de manera sencilla y organizada.
















D =Principio de inversión de la dependencia (Dependency inversion principle)
la noción de que se debe “depender de abstracciones, no depender de implementaciones”.[4]​
La Inyección de Dependencias es uno de los métodos que siguen este principio.
