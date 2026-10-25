# Pascal — Cálculo numérico y conversión de bases

Proyectos académicos en Pascal sobre representación de números en distintas bases, normalización en punto flotante, truncamiento y redondeo. La carpeta incluye un programa de consola y el código de una unidad gráfica de Lazarus.

Estos ejercicios prácticos fueron realizados durante el cursado de diversas materias mientras estudiaba la **Licenciatura en Análisis de Sistemas (Plan 2010)** de la **Universidad Nacional de Salta**.

**Materia:** ______________________________

## Contenido

- [Estructura](#estructura)
- [Conversor de bases](#conversor-de-bases)
- [Normalización de números](#normalización-de-números)
- [Compilación y uso](#compilación-y-uso)
- [Estado y validación](#estado-y-validación)
- [Licencia](#licencia)

## Estructura

```text
.
├── Numerical Calculus/
│   ├── ConversordeBases.pas
│   └── NormalizaciondeNumeros.pas
├── LICENSE
└── README.md
```

## Conversor de bases

[ConversordeBases.pas](Numerical%20Calculus/ConversordeBases.pas) declara el programa de consola `TrabajoNumerica`. Solicita un número, su base y su exponente, y ofrece convertirlo a otra base entre `2` y `16`.

El código trabaja con las partes entera y fraccionaria almacenadas como cadenas, y utiliza los caracteres `0` a `9` y `A` a `F` para representar dígitos. La estructura `tNumero` almacena las partes del número, la base, el exponente y un campo de signo.

| Grupo de funciones | Propósito |
| --- | --- |
| `busqueda` y `control` | Comprobación de los caracteres ingresados según la base. |
| `sumaPonderada` | Conversión hacia base decimal mediante pesos de las posiciones. |
| `divisionReiterada` y `multReiterada` | Conversión de las partes entera y fraccionaria mediante divisiones y multiplicaciones sucesivas. |
| `C_Punto_Flotante`, `DevuelveNumConExp0` y `convertPFsinN` | Transformaciones de la representación y de su exponente. |
| `Redondeo` y `Corte` | Presentación con una cantidad de dígitos de precisión mediante redondeo o truncamiento. |
| `Carga_Numero`, `Menu` y `Menu1` | Entrada de datos y selección de opciones en consola. |

La versión de consola reserva hasta diez caracteres para la parte entera y treinta y dos para la parte decimal. Es una implementación de estudio con límites de representación y conversiones auxiliares a tipos numéricos; esos tamaños no garantizan que cualquier valor dentro de ellos pueda convertirse correctamente.

## Normalización de números

[NormalizaciondeNumeros.pas](Numerical%20Calculus/NormalizaciondeNumeros.pas) contiene la unidad Object Pascal `Unit1`, en modo `objfpc`, para una interfaz gráfica de Lazarus.

Declara el formulario `TventPrinc` con campos para el número, la base y el exponente, controles de base de destino y precisión, y etiquetas para presentar el número original y las formas convertida, normalizada, truncada y redondeada. La lógica se conecta al evento `btnConvClick`.

Esta unidad utiliza la biblioteca de componentes de Lazarus y referencia un recurso de formulario con `{$R *.lfm}`. El repositorio no incluye el `.lfm`, un programa principal `.lpr` ni un proyecto `.lpi`. Por tanto, la unidad gráfica requiere reconstruir o recuperar el proyecto y el formulario antes de poder ejecutarse. También hay que hacer coincidir el nombre de archivo de la unidad con `Unit1` al integrarla en Lazarus.

## Compilación y uso

### Requisitos

- Free Pascal para el programa de consola. La compilación documentada utiliza el modo Object Pascal.
- Lazarus y sus componentes gráficos para recuperar la versión con formulario.
- Una terminal interactiva para la aplicación de consola, que utiliza la unidad `crt`.

Los comandos siguientes usan Bash y se ejecutan desde la raíz del repositorio:

```bash
git clone https://github.com/GabrielUnsa/Pascal.git
cd Pascal
mkdir -p build
fpc -Mobjfpc -FEbuild -FUbuild -obuild/conversor \
  "Numerical Calculus/ConversordeBases.pas"
./build/conversor
```

`-Mobjfpc` permite la sintaxis Object Pascal que utiliza el código, incluido el identificador `Result`. Las opciones `-FE`, `-FU` y `-o` dirigen el ejecutable y los archivos de compilación a `build/`.

### Flujo de la consola

1. Ingresar el número. Para explorar las fracciones, utilizar el punto como separador y comenzar con valores pequeños.
2. Indicar la base de origen y el exponente.
3. Responder al menú de conversión y elegir una base de destino entre `2` y `16`.
4. Cuando el programa lo solicite, indicar la cantidad de dígitos para el redondeo y el truncamiento.
5. Revisar las representaciones impresas y pulsar Enter al finalizar.

Si el número se considera inválido, el programa permite volver a ingresarlo o escribir `SALIR` en ese paso de validación. No hay un menú global de salida con ese comando.

## Estado y validación

El conversor de consola se compiló correctamente con **Free Pascal 3.2.2 en Linux**, usando `-Mobjfpc`. El compilador emitió advertencias por variables locales que podrían no estar inicializadas. Sin seleccionar ese modo, la compilación en el entorno de prueba falló por el uso de `Result`.

La verificación realizada cubre la compilación. No se validaron de forma exhaustiva los resultados de conversión, los signos, los exponentes ni los casos límite de precisión. La versión gráfica no se compiló porque faltan los archivos de proyecto y formulario.

El código conserva diferencias entre la validación y el procesamiento de separadores decimales, accesos a cadenas que requieren revisar sus índices y cálculos auxiliares sujetos a límites de tipos numéricos. Conviene contrastar los resultados con ejemplos conocidos al estudiar o modificar los algoritmos. No se incluyen pruebas automatizadas.

## Licencia

Distribuido bajo la [licencia MIT](LICENSE). Copyright © 2025 Gabriel Marmanillo.
