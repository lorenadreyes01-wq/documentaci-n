# Principios SOLID y Refactorización en C#

**Autor:** Lorena Durán
**Curso:** 5to de Informática B
**Asignatura:** Programación
**Fecha:** Junio 2026

---

# Índice

1. Introducción
2. Representación de los Principios SOLID
3. ¿Qué significa SOLID?
4. Importancia de SOLID en la Programación Orientada a Objetos
5. Conceptos Clave
6. Práctica de Refactorización

   * Parte 1: SRP
   * Parte 2: OCP
   * Parte 3: LSP
   * Parte 4: ISP
   * Parte 5: DIP
7. Reflexión Final
8. Conclusión
9. Referencias

---

# Introducción

Los principios SOLID son un conjunto de buenas prácticas utilizadas en la Programación Orientada a Objetos para diseñar software más limpio, organizado y fácil de mantener. Estos principios ayudan a reducir errores, mejorar la reutilización del código y facilitar el crecimiento de los proyectos a largo plazo.

---

# Representación de los Principios SOLID

![Diagrama de los Principios SOLID](https://click-it.es/wp-content/uploads/2021/08/Untitled-7.jpg)

*Figura 1. Representación visual de los principios SOLID.*

---

# ¿Qué significa SOLID?

| Letra | Principio                       | Descripción                                                                                        |
| ----- | ------------------------------- | -------------------------------------------------------------------------------------------------- |
| S     | Single Responsibility Principle | Una clase debe tener una sola responsabilidad.                                                     |
| O     | Open/Closed Principle           | El software debe estar abierto para extensión y cerrado para modificación.                         |
| L     | Liskov Substitution Principle   | Las clases hijas deben poder sustituir a las clases padres sin alterar el comportamiento esperado. |
| I     | Interface Segregation Principle | Las clases no deben depender de métodos que no utilizan.                                           |
| D     | Dependency Inversion Principle  | Las clases deben depender de abstracciones y no de implementaciones concretas.                     |

---

# Importancia de SOLID en la Programación Orientada a Objetos

SOLID permite desarrollar sistemas más organizados y preparados para crecer. Cuando estos principios se aplican correctamente, el software es más fácil de modificar y mantener.

## Beneficios

* Facilita el mantenimiento del código.
* Reduce el acoplamiento entre clases.
* Favorece la reutilización de componentes.
* Permite escalar proyectos con mayor facilidad.
* Mejora la realización de pruebas unitarias.
* Facilita el trabajo colaborativo entre desarrolladores.

## Problemas cuando no se utiliza SOLID

* Clases demasiado grandes.
* Código difícil de entender.
* Mayor cantidad de errores.
* Dificultad para agregar nuevas funcionalidades.
* Dependencias excesivas entre componentes.

---

# Conceptos Clave

## Acoplamiento

Es el grado de dependencia que existe entre dos o más clases. Un alto acoplamiento significa que un cambio en una clase puede afectar directamente a otras. Lo recomendable es mantener un bajo acoplamiento para lograr sistemas más flexibles.

## Cohesión

Es el nivel de relación entre las responsabilidades de una clase. Una clase con alta cohesión tiene funciones relacionadas con un único propósito específico.

## Refactorización

Es el proceso de mejorar la estructura interna del código sin modificar su comportamiento externo. Su objetivo es hacer el código más limpio y mantenible.

## Escalabilidad

Es la capacidad de un sistema para crecer y adaptarse a nuevas necesidades sin afectar significativamente su funcionamiento.

## Mantenibilidad

Es la facilidad con la que un software puede corregirse, actualizarse o mejorarse con el paso del tiempo.

## Abstracción

Consiste en representar únicamente las características esenciales de un objeto, ocultando detalles innecesarios de implementación.

## Dependencias

Son los componentes, objetos o servicios que una clase necesita para realizar sus funciones correctamente.

---

# Práctica de Refactorización

# Parte 1 — Single Responsibility Principle (SRP)

## Código Refactorizado

```csharp
using System;

public class GeneradorReporte
{
    public void GenerarReporte()
    {
        Console.WriteLine("Generando reporte...");
    }
}

public class GestorArchivo
{
    public void GuardarEnArchivo()
    {
        Console.WriteLine("Guardando archivo...");
    }
}

public class ServicioCorreo
{
    public void EnviarCorreo()
    {
        Console.WriteLine("Enviando correo...");
    }
}
```

## Análisis

### ¿Qué problema tenía el diseño original?

La clase original realizaba varias tareas diferentes: generar reportes, guardar archivos y enviar correos. Esto viola el principio de responsabilidad única.

### ¿Qué ventajas aporta la refactorización?

* Mayor organización.
* Código más limpio.
* Mejor mantenimiento.
* Menor probabilidad de errores.

### ¿Qué ocurriría si el sistema crece?

Sería más sencillo agregar nuevas funcionalidades sin afectar otras partes del sistema.

---

# Parte 2 — Open/Closed Principle (OCP)

## Código Refactorizado

```csharp
using System;

public interface IDescuento
{
    double Calcular(double monto);
}

public class DescuentoRegular : IDescuento
{
    public double Calcular(double monto)
    {
        return monto * 0.05;
    }
}

public class DescuentoVIP : IDescuento
{
    public double Calcular(double monto)
    {
        return monto * 0.10;
    }
}

public class DescuentoPremium : IDescuento
{
    public double Calcular(double monto)
    {
        return monto * 0.15;
    }
}
```

## Análisis

### ¿Por qué este código no era escalable?

Porque cada nuevo tipo de cliente requería modificar la clase original.

### ¿Cómo ayuda el polimorfismo?

Permite que cada tipo de descuento implemente su propia lógica utilizando la misma interfaz.

### ¿Qué ventaja ofrece OCP en proyectos grandes?

Facilita agregar nuevas funcionalidades sin modificar código ya existente.

---

# Parte 3 — Liskov Substitution Principle (LSP)

## Código Refactorizado

```csharp
using System;

public class Ave
{
    public void Comer()
    {
        Console.WriteLine("Comiendo...");
    }
}

public interface IAveVoladora
{
    void Volar();
}

public class Paloma : Ave, IAveVoladora
{
    public void Volar()
    {
        Console.WriteLine("La paloma está volando.");
    }
}

public class Pinguino : Ave
{
    public void Nadar()
    {
        Console.WriteLine("El pingüino está nadando.");
    }
}
```

## Análisis

### ¿Por qué el pingüino viola LSP?

Porque hereda un comportamiento que no puede realizar correctamente.

### ¿Qué riesgos genera esto?

Puede producir errores inesperados durante la ejecución del programa.

### ¿Cómo mejorarías la jerarquía?

Separando las capacidades mediante interfaces específicas.

---

# Parte 4 — Interface Segregation Principle (ISP)

## Código Refactorizado

```csharp
using System;

public interface ITrabajador
{
    void Trabajar();
}

public interface IComedor
{
    void Comer();
}

public class Empleado : ITrabajador, IComedor
{
    public void Trabajar()
    {
        Console.WriteLine("Trabajando...");
    }

    public void Comer()
    {
        Console.WriteLine("Comiendo...");
    }
}

public class Robot : ITrabajador
{
    public void Trabajar()
    {
        Console.WriteLine("Trabajando...");
    }
}
```

## Análisis

### ¿Qué problema presenta esta interfaz?

Obliga a algunas clases a implementar métodos que no necesitan.

### ¿Cómo mejora ISP el diseño?

Cada clase implementa únicamente las interfaces necesarias.

### ¿Qué ventajas ofrece dividir interfaces?

* Mayor flexibilidad.
* Menor acoplamiento.
* Mejor organización.

---

# Parte 5 — Dependency Inversion Principle (DIP)

## Código Refactorizado

```csharp
using System;

public interface IBaseDatos
{
    void Guardar();
}

public class MySQLDatabase : IBaseDatos
{
    public void Guardar()
    {
        Console.WriteLine("Guardando en MySQL");
    }
}

public class SQLServerDatabase : IBaseDatos
{
    public void Guardar()
    {
        Console.WriteLine("Guardando en SQL Server");
    }
}

public class UsuarioService
{
    private IBaseDatos db;

    public UsuarioService(IBaseDatos db)
    {
        this.db = db;
    }

    public void CrearUsuario()
    {
        db.Guardar();
    }
}
```

## Análisis

### ¿Por qué el acoplamiento es un problema?

Porque obliga a depender de una implementación específica.

### ¿Qué ventajas ofrece depender de abstracciones?

Permite cambiar implementaciones sin modificar la lógica principal.

### ¿Cómo ayuda DIP en pruebas unitarias?

Permite utilizar objetos simulados para realizar pruebas sin depender de sistemas reales.

---

# Reflexión Final

## ¿Cuál principio SOLID consideras más difícil?

Considero que el principio de Sustitución de Liskov es el más complejo porque requiere diseñar cuidadosamente las relaciones de herencia para evitar comportamientos incorrectos.

## ¿Cuál crees que aporta más valor?

Pienso que el principio de Responsabilidad Única aporta mucho valor porque ayuda a mantener el código organizado desde el inicio.

## ¿Cómo cambiaría tu manera de programar después de esta actividad?

Intentaría planificar mejor mis clases y distribuir correctamente las responsabilidades antes de comenzar a programar.

## ¿Qué diferencias notas entre un código rápido y un código bien diseñado?

Un código rápido suele resolver el problema inmediato, pero puede volverse difícil de mantener. Un código bien diseñado es más limpio, reutilizable, escalable y fácil de entender.

---

# Conclusión

Los principios SOLID son fundamentales para el desarrollo de software moderno. Su aplicación permite construir sistemas más robustos, mantenibles y preparados para crecer. Además, facilitan el trabajo en equipo y reducen la posibilidad de errores durante la evolución de un proyecto.

---

# Referencias

* https://learn.microsoft.com/es-es/dotnet/csharp/
* https://refactoring.guru/es/design-patterns
* https://es.wikipedia.org/wiki/SOLID

---

# Imagen adicional

![Arquitectura de Software](https://chatgpt.com/backend-api/estuary/content?id=file_000000000dac71fdb2fc689332861590&ts=494584&p=fsns&cid=1&sig=dbd9b29b46427293e0bf8a2fb55f76e07292a50546f9f23ed54f0e9414495028&v=0)

*Figura 2. Ejemplo de una arquitectura organizada aplicando principios SOLID.*
