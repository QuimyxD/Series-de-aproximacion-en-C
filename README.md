# Cálculo de Series en C: Aproximación Numérica y Análisis de Rendimiento

[![C Language](https://img.shields.io/badge/Language-C99%20%2F%20C11-blue.svg)](https://en.wikipedia.org/wiki/C_(programming_language))
[![Build System](https://img.shields.io/badge/CMake-3.10%2B-green.svg)](https://cmake.org/)
[![Documentation](https://img.shields.io/badge/Docs-Doxygen-brightgreen.svg)](https://www.doxygen.nl/)
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

Implementación y análisis numérico de 33 series matemáticas en C mediante el uso de estructuras de control (`for`, `while`, `do-while`). Este proyecto aborda desde aproximaciones directas hasta la optimización algorítmica por relaciones de recurrencia, incluyendo un estudio de convergencia, métricas de error de aproximación y comparación de rendimiento entre estrategias iterativas.

---

## Tabla de Contenidos

- [Características Destacadas](#-características-destacadas)
- [Arquitectura y Niveles de Implementación](#-arquitectura-y-niveles-de-implementación)
- [Estructura del Proyecto](#-estructura-del-proyecto)
- [Catálogo de las 33 Funciones Matemáticas](#-catálogo-de-las-33-funciones-matemáticas)
- [Instrucciones de Compilación y Ejecución](#-instrucciones-de-compilación-y-ejecución)
  - [Requisitos Previos](#requisitos-previos)
  - [Método 1: Compilación Automatizada con CMake (Recomendado)](#método-1-compilación-automatizada-con-cmake-recomendado)
  - [Método 2: Compilación Manual con GCC](#método-2-compilación-manual-con-gcc)
- [Documentación Técnica](#-documentación-técnica)
- [Licencia](#-licencia)

---

## Características Destacadas

* **Evolución por Niveles de Rendimiento:** Transición progresiva desde algoritmos directos $\mathcal{O}(n^2)$ hasta optimizaciones por recurrencia en tiempo lineal $\mathcal{O}(n)$.
* **Análisis de Error y Estabilidad:** Cálculo de diferencia paso a paso ($\Delta_n$) y seguimiento detallado del error de aproximación numérico.
* **Validación de Dominio:** Restricción estricta de parámetros para garantizar convergencia matemática en funciones trigonométricas, logarítmicas y exponenciales.
* **Documentación Doxygen:** Cobertura de código documentada con salidas automatizadas en formatos HTML y LaTeX/PDF.

---

## Arquitectura y Niveles de Implementación

El proyecto se divide estructuralmente en tres fases de optimización y madurez de software:

1. **Nivel 1 (Inicial):** Solución directa recalculando factoriales y potencias desde cero en cada término. Complejidad computacional $\mathcal{O}(n^2)$.
2. **Nivel 2 (Intermedio):** Estabilización, validación estricta de dominios de definición y evaluación de convergencia para $n \in \{2, 4, 8, 16, 32, 64, 128, 256\}$.
3. **Nivel 3 (Avanzado):** Optimización mediante relaciones de recurrencia ($\mathcal{O}(n)$), eliminación de redundancias numéricas, métricas de $\Delta_n$, error relativo y generación automatizada de documentación.

---

## Estructura del Proyecto

```text
series-approximation-c/
│
├── .gitignore
├── .gitattributes           # Reglas de Linguist para estadísticas de GitHub.               
├── CMakeLists.txt           # Configuración principal de compilación para el proyecto.
├── LICENSE                  
├── README.md                  
│
├── Nivel1_Inicial/          # NIVEL 1: SOLUCIÓN DIRECTA
│   └── main_nivel1.c        # Un solo archivo con las 33 series implementadas de forma simple, O(n²).
│                            
├── Nivel2_Intermedio/       # NIVEL 2: ESTABILIZACIÓN Y VALIDACIÓN
│   ├── include/             
│   │   └── series_v2.h      # Declaración de las 33 series y macros de validación.
│   ├── src/                 
│   │   ├── constantes.c     # Series 1-6 y 27-33.
│   │   ├── exponenciales.c  # Series 7-13.
│   │   └── trigonometricas.c # Series 19-26.            
│   └── main_nivel2.c        # Validación de dominio. Genera tablas con n={2,4,8,16,32,64,128,256}.
│
└── Nivel3_Avanzado/         # NIVEL 3: OPTIMIZACIÓN Y DOCUMENTACIÓN
|   ├── html/                # Documentación web interactiva generada automáticamente por Doxygen.
|   ├── include/             
|   │   └── series_v3.h      # Headers documentados con estándares Doxygen.
|   ├── latex/               # Documentación en formato PDF/LaTeX generada por Doxygen.
|   ├── src/                 
|   │   ├── especial_opt.c   # Implementación optimizada de funciones especiales.
|   │   └── trig_exp_opt.c   # Funciones trigonométricas y exponenciales por recurrencia O(n).            
|   └── main_nivel3.c        # Cálculo de métricas: Delta_n (diferencia) y Error de Aproximación.
|
|__ Reporte/                 # Reporte del código.
     |__ Reporte.pdf 

```

---

## Catálogo de las 33 Funciones Matemáticas

A continuación se listan las series matemáticas que componen este proyecto, implementadas y analizadas a través de los tres niveles de optimización algorítmica:

1. **Logaritmo natural de 2:**
   $$\ln(2) = 1 - \frac{1}{2} + \frac{1}{3} - \frac{1}{4} + \dots$$
2. **Pi cuartos:**
   $$\frac{\pi}{4} = 1 - \frac{1}{3} + \frac{1}{5} - \frac{1}{7} + \dots$$
3. **Pi cuadrado sobre 6:**
   $$\frac{\pi^2}{6} = 1 + \frac{1}{2^2} + \frac{1}{3^2} + \dots$$
4. **Pi cuadrado sobre 8:**
   $$\frac{\pi^2}{8} = 1 + \frac{1}{3^2} + \frac{1}{5^2} + \dots$$
5. **Serie para 1/2:**
   $$\sum_{n=0}^{\infty} \frac{1}{(2n+1)(2n+3)}$$
6. **Serie para 3/4:**
   $$\sum_{n=1}^{\infty} \frac{1}{n(n+2)}$$
7. **Función exponencial:**
   $$e^x = 1 + x + \frac{x^2}{2!} + \frac{x^3}{3!} + \dots$$
8. **Serie para $xe^x$:**
   $$x + \frac{2x^2}{2!} + \frac{3x^3}{3!} + \dots$$
9. **Serie para $(x+x^2)e^x$:**
   $$x + \frac{4x^2}{2!} + \frac{9x^3}{3!} + \dots$$
10. **Logaritmo natural de $1+x$:**
    $$\ln(1+x) = x - \frac{x^2}{2} + \frac{x^3}{3} - \dots \quad \text{para } -1 < x \le 1$$
11. **Variante Logarítmica:**
    $$\frac{1}{2}\ln\left(\frac{1+x}{1-x}\right) = x + \frac{x^3}{3} + \frac{x^5}{5} + \dots \quad \text{para } -1 < x < 1$$
12. **Logaritmo de $x$ (Forma 1):**
    $$2\left(\frac{x-1}{x+1}\right) + \frac{1}{3}\left(\frac{x-1}{x+1}\right)^3 + \dots \quad \text{para } x > 0$$
13. **Logaritmo de $x$ (Forma 2):**
    $$\left(\frac{x-1}{x}\right) + \frac{1}{2}\left(\frac{x-1}{x}\right)^2 + \dots \quad \text{para } x \ge \frac{1}{2}$$
14. **Teorema del Binomio:**
    $$(1+x)^\alpha = \binom{\alpha}{0} + \binom{\alpha}{1}x + \binom{\alpha}{2}x^2 + \dots \quad \text{para } |x| < 1$$
15. **Función potencia $a^x$:**
    $$a^x = 1 + x\ln a + \frac{(x\ln a)^2}{2!} + \dots \quad \text{para } a > 0$$
16. **Números de Bernoulli ($B_k$):**
    $$B_k = -\sum_{i=0}^{k-1} \binom{k}{i} \frac{B_i}{k+1-i}$$
17. **Números de Euler ($E_k$):**
    $$E_k = \frac{2^{2k+2}(2k)!}{\pi^{2k+1}} \left( 1 - \frac{1}{3^{2k+1}} + \frac{1}{5^{2k+1}} - \dots \right)$$
18. **Números de Euler ($E_{2k}$):**
    $$E_{2k} = i \sum_{m=1}^{2k+1} \sum_{j=0}^{m} \binom{m}{j} (-1)^j \frac{(m-2j)^{2k+1}}{2^m i m}$$
19. **Seno:**
    $$\sin x = x - \frac{x^3}{3!} + \frac{x^5}{5!} - \dots$$
20. **Coseno:**
    $$\cos x = 1 - \frac{x^2}{2!} + \frac{x^4}{4!} - \dots$$
21. **Tangente:**
    $$\tan x \quad \text{(con coeficientes } B_{2n}\text{) para } |x| < \frac{\pi}{2}$$
22. **Secante:**
    $$\sec x \quad \text{(con coeficientes } E_{2n}\text{) para } |x| < \frac{\pi}{2}$$
23. **Cosecante:**
    $$\csc x \quad \text{para } 0 < |x| < \pi$$
24. **Arcoseno:**
    $$\arcsin x = x + \frac{1}{2}\frac{x^3}{3} + \frac{1\cdot 3}{2\cdot 4}\frac{x^5}{5} + \dots \quad \text{para } |x| < 1$$
25. **Arcocoseno:**
    $$\arccos x = \frac{\pi}{2} - \arcsin x \quad \text{para } |x| < 1$$
26. **Arcotangente:**
    $$\arctan x \quad \text{(Series distintas para } |x| < 1 \text{ y } |x| \ge 1\text{)}$$
27. **Seno hiperbólico:**
    $$\sinh x = x + \frac{x^3}{3!} + \frac{x^5}{5!} + \dots$$
28. **Coseno hiperbólico:**
    $$\cosh x = 1 + \frac{x^2}{2!} + \frac{x^4}{4!} + \dots$$
29. **Tangente hiperbólica:**
    $$\tanh x \quad \text{para } |x| < \frac{\pi}{2}$$
30. **Arcoseno hiperbólico:**
    $$\operatorname{arcsenh} x = x - \frac{1}{6}x^3 + \frac{3}{40}x^5 - \dots \quad \text{para } |x| < 1$$
31. **Arcotangente hiperbólica:**
    $$\operatorname{arctanh} x = x + \frac{x^3}{3} + \frac{x^5}{5} + \dots \quad \text{para } |x| < 1$$
32. **Serie combinada:**
    $$\frac{\ln(1+x)}{1+x} = x - \left(1+\frac{1}{2}\right)x^2 + \left(1+\frac{1}{2}+\frac{1}{3}\right)x^3 - \dots$$
33. **Exponencial del seno:**
    $$e^{\sin x} = 1 + x + \frac{x^2}{2} - \frac{x^4}{8} - \dots$$

---

## Instrucciones de Compilación y Ejecución

Este proyecto utiliza **CMake** como sistema de construcción para garantizar portabilidad entre distintos sistemas operativos (Windows, macOS, Linux).

### Requisitos Previos

* Compilador de C estándar compatible con C99 o superior (`gcc`, `clang` o MSVC).
* **CMake** (versión 3.10 o superior).
* Doxygen *(Opcional, para regenerar la documentación técnica)*.

---

### Método 1: Compilación Automatizada con CMake (Recomendado)

Desde la raíz del proyecto, ejecuta los siguientes comandos en tu terminal para compilar el módulo optimizado (**Nivel 3**):

```bash
# 1. Crear un directorio aislado para los binarios
mkdir build
cd build

# 2. Generar los archivos de configuración
cmake ..

# 3. Compilar el código fuente
cmake --build .
```

#### Ejecución del binario resultante:

* **Linux / macOS:**
  ```bash
  ./Nivel3_Avanzado/main_nivel3
  ```
* **Windows (CMD / PowerShell):**
  ```cmd
  .\Nivel3_Avanzado\Debug\main_nivel3.exe
  ```

---

### Método 2: Compilación Manual con GCC

Si no dispones de CMake instalado, puedes compilar el proyecto directamente con `gcc` enlazando la librería matemática (`-lm`):

```bash
# Compilar especificando directorios de inclusión y código fuente del Nivel 3
gcc Nivel3_Avanzado/src/*.c Nivel3_Avanzado/main_nivel3.c -I Nivel3_Avanzado/include -o main_nivel3 -lm

# Ejecutar el binario generado
./main_nivel3
```

---

## Documentación Técnica

La documentación del código está estandarizada con formato **Doxygen**:
* La documentación en **HTML** se encuentra en `Nivel3_Avanzado/html/index.html`. Puedes abrirla con cualquier navegador web.
* El soporte para documentación en **LaTeX / PDF** está disponible dentro del directorio `Nivel3_Avanzado/latex/`.

---

## Autor y Créditos

**Cecil Quimey Azuara Yáñez**

- **Carrera:** Licenciatura en Ingeniería de Datos e Inteligencia Artificial (LIDIA).
- **Institución:** Universidad de Guanajuato – División de Ingenierías (Campus Irapuato - Salamanca).
- **Asignatura:** Fundamentos del Análisis de Datos.
