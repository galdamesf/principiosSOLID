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

