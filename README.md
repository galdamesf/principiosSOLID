# 📘 Principios SOLID en Java

📚 **Breve introducción a los Principios SOLID en Java**  
Una vez que dominamos los fundamentos de la Programación Orientada a Objetos (POO) —como clases, objetos, atributos, métodos, encapsulamiento, constructores y getters/setters—, es importante comenzar a pensar en cómo escribir código limpio, mantenible y escalable.

Ahí es donde entran los principios SOLID.

**SOLID** es un conjunto de 5 buenas prácticas que te ayudan a construir software más robusto. No necesitas dominarlos al 100% al inicio, pero sí comenzar a entender su propósito.

En la siguiente sección, exploraremos cada principio de forma simple y con ejemplos en Java, para que puedas aplicar estas ideas paso a paso a medida que avanzas como desarrollador.

Los principios SOLID son cinco reglas fundamentales de diseño en la programación orientada a objetos. Fueron definidos por Robert C. Martin ("Uncle Bob") y ayudan a escribir código más limpio, mantenible, escalable y fácil de entender.

A continuación, te presentamos una versión simplificada y didáctica de cada principio, con analogías reales y ejemplos en Java para que puedas comprenderlos fácilmente:

# La letra 'S' de 'SOLID' en el desarrollo de software representa el principio de:

Single Responsibility Principle (SRP)
o en español: Principio de Responsabilidad Única.

✅ ¿Qué significa?
Una clase (o módulo, función, etc.) debe tener una sola razón para cambiar, es decir, una única responsabilidad.

📌 Explicación simple
Imagina que tienes una máquina de café que además de hacer café, también imprime facturas y gestiona los turnos de los empleados. Si se rompe algo, no sabes si fue por el café, por la impresora o por el sistema de turnos. Es muy difícil de mantener y arreglar.

En cambio, si tienes:

Una clase para preparar café,

Otra clase para imprimir facturas,

Y otra para gestionar turnos...

Cada una tiene una sola tarea clara, y puedes modificar una sin afectar las otras.

🛠️ En código Java (ejemplo simple)
Violando SRP:

java
Copiar
Editar
public class Reporte {
    public String generarReporte() {
        // Generar reporte
    }

    public void guardarEnArchivo(String reporte) {
        // Guardar en archivo
    }

    public void enviarPorEmail(String reporte) {
        // Enviar por email
    }
}
Aplicando SRP:

java
Copiar
Editar
public class Reporte {
    public String generarReporte() {
        // Generar reporte
    }
}

public class Guardador {
    public void guardarEnArchivo(String reporte) {
        // Guardar en archivo
    }
}

public class Enviador {
    public void enviarPorEmail(String reporte) {
        // Enviar por email
    }
}
🧠 Ventajas de aplicar SRP
Código más legible y modular

Fácil de mantener y extender

Menos riesgo de errores al cambiar una parte




# La letra 'O' de 'SOLID' en el desarrollo de software representa el principio de:

Open/Closed Principle (OCP)
o en español: Principio Abierto/Cerrado.

✅ ¿Qué significa?
Las entidades de software (clases, módulos, funciones, etc.) deben estar abiertas para extensión pero cerradas para modificación. Esto significa que el comportamiento de una clase debe ser extensible sin modificar su código fuente.

📌 Explicación simple
Imagina que tienes una aplicación de procesamiento de imágenes que puede aplicar filtros a las imágenes. Si quieres agregar un nuevo filtro, no deberías tener que modificar el código existente. En su lugar, deberías poder extender la funcionalidad existente sin tocar el código original.

En cambio, si tienes:

Una clase base que define una interfaz para aplicar filtros,

Y clases derivadas para cada tipo de filtro específico...

Puedes agregar nuevos filtros simplemente creando nuevas clases derivadas sin modificar la clase base.

🛠️ En código Java (ejemplo simple)

Violando OCP:

java

public class ImageProcessor {
    public void applyFilter(Image image, String filterType) {
        if ("brightness".equals(filterType)) {
            // Aplicar filtro de brillo
        } else if ("contrast".equals(filterType)) {
            // Aplicar filtro de contraste
        }
        // Más filtros...
    }
}

Aplicando OCP:

java

public interface Filter {
    void apply(Image image);
}

public class BrightnessFilter implements Filter {
    public void apply(Image image) {
        // Aplicar filtro de brillo
    }
}

public class ContrastFilter implements Filter {
    public void apply(Image image) {
        // Aplicar filtro de contraste
    }
}

public class ImageProcessor {
    private List<Filter> filters = new ArrayList<>();

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

La letra 'L' de 'SOLID' en el desarrollo de software representa el principio de:

# El Principio de Sustitución de Liskov (LSP) suele ser el más confuso de los SOLID! Vamos a destriparlo con ejemplos claros y situaciones cotidianas para que quede cristalino.

🔍 ¿Qué dice el LSP?
📌 "Si una clase B es hija de una clase A, entonces deberíamos poder usar B en cualquier lugar donde usamos A sin que el programa se comporte de manera inesperada."

En otras palabras:

Los hijos no deben romper las promesas de los padres.

No deben modificar comportamientos base de forma radical.

🌟 Ejemplo Intuitivo: Figuras Geométricas
✅ Caso Correcto (Cumple LSP):
java
class Rectángulo {
    protected int ancho, alto;
    
    void setAncho(int ancho) { this.ancho = ancho; }
    void setAlto(int alto) { this.alto = alto; }
    int calcularArea() { return ancho * alto; }
}

class Cuadrado extends Rectángulo {
    @Override
    void setAncho(int ancho) {
        this.ancho = ancho;
        this.alto = ancho; // En un cuadrado, ancho = alto
    }
    
    @Override
    void setAlto(int alto) {
        this.alto = alto;
        this.ancho = alto; // En un cuadrado, alto = ancho
    }
}
¿Por qué funciona?

Un Cuadrado es un Rectángulo (matemáticamente cierto).

Si en tu código esperas un Rectángulo y recibes un Cuadrado, no hay sorpresas: el área se calcula igual (ancho * alto).

❌ Caso Incorrecto (Violación del LSP):
Imagina que el Cuadrado sobrescribe calcularArea() para devolver siempre ancho * ancho (ignorando el alto):

java
class Cuadrado extends Rectángulo {
    @Override
    int calcularArea() {
        return ancho * ancho; // ¡Rompe la lógica de Rectángulo!
    }
}
Problema:

Si otro código espera que calcularArea() de un Rectángulo sea ancho * alto, al recibir un Cuadrado, ¡el resultado será incorrecto!

El hijo (Cuadrado) alteró una funcionalidad crítica del padre (Rectángulo).

🚨 Ejemplo Realista: Violación Común
Caso: Sistema de Pagos
java
class TarjetaCredito {
    void pagar(double monto) {
        if (monto <= 0) throw new Error("Monto inválido");
        // Lógica de pago...
    }
}

class TarjetaRegalo extends TarjetaCredito {
    @Override
    void pagar(double monto) {
        if (monto > 100) throw new Error("Límite excedido"); // ¡Nueva restricción!
    }
}
¿Por qué viola LSP?

Si un módulo espera una TarjetaCredito y le pasas una TarjetaRegalo, ¡puede fallar con montos >100!

El hijo añadió una condición que el padre no tiene, rompiendo la sustituibilidad.

🔧 Cómo Cumplir con LSP
Los hijos no deben fortalecer precondiciones (exigir más que el padre).

Ejemplo: Si el padre acepta monto > 0, el hijo no puede exigir monto > 10.

Los hijos no deben debilitar postcondiciones (prometer menos que el padre).

Ejemplo: Si el padre garantiza que pagar() guarda un registro en BD, el hijo no puede omitirlo.

Los hijos deben mantener invariantes (reglas internas de la clase padre).

Ejemplo: Si en Rectángulo ancho != alto, entonces Cuadrado no debería heredar de él.

📜 Regla Mnemotécnica para LSP
"Si parece un pato, grazna como un pato, pero necesita baterías… no es un pato."
– Adaptación del Duck Test.

En código:

Si una subclase necesita hacks para funcionar como la superclase, probablemente viola LSP.

✅ Ejemplo de Diseño LSP-Friendly
java
interface Forma {
    double calcularArea();
}

class Rectángulo implements Forma { ... } // Tiene ancho y alto
class Cuadrado implements Forma { ... }   // Solo tiene lado
Clave:

No hay herencia entre Rectángulo y Cuadrado.

Ambos implementan Forma, pero no se sustituyen entre sí.

📊 Resumen LSP en una Tabla
Situación	Cumple LSP?	Por qué
Hijo no altera contratos	✅ Sí	Comportamiento predecible.
Hijo añade excepciones	❌ No	Rompe sustitución.
Hijo relaja condiciones	❌ No	El padre no lo permitiría.
🛠 Consecuencias de Violar LSP
Bugs silenciosos: Fallos que aparecen solo al usar subclases.

Código frágil: Cambios en el padre pueden romper hijos (y viceversa).

Difícil testing: Mocks y tests deben considerar todas las variantes de herencia.
